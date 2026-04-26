<script setup lang="ts">
import {
  computed,
  onBeforeUnmount,
  onMounted,
  ref,
  useTemplateRef,
  watch,
  type CSSProperties
} from "vue";

type ElectricBorderProps = {
  color?: string;
  speed?: number;
  chaos?: number;
  thickness?: number;
  className?: string;
  style?: CSSProperties;
};

const props = withDefaults(defineProps<ElectricBorderProps>(), {
  color: "#28FF85",
  speed: 1,
  chaos: 1,
  thickness: 2
});

// ✅ DETECT MOBILE
const isMobile = ref(false);

onMounted(() => {
  isMobile.value = window.innerWidth < 768;
});

// ==========================
// UTIL
// ==========================
function hexToRgba(hex: string, alpha = 1): string {
  if (!hex) return `rgba(0,0,0,${alpha})`;
  let h = hex.replace("#", "");
  if (h.length === 3) {
    h = h
      .split("")
      .map(c => c + c)
      .join("");
  }
  const int = parseInt(h, 16);
  const r = (int >> 16) & 255;
  const g = (int >> 8) & 255;
  const b = int & 255;
  return `rgba(${r}, ${g}, ${b}, ${alpha})`;
}

const rawId = `id-${crypto.randomUUID().replace(/[:]/g, "")}`;
const filterId = `turbulent-displace-${rawId}`;

const svgRef = useTemplateRef("svgRef");
const rootRef = useTemplateRef("rootRef");
const strokeRef = useTemplateRef("strokeRef");

// ==========================
// ANIMATION
// ==========================
const updateAnim = () => {
  if (isMobile.value) return; // ❌ skip di mobile

  const svg = svgRef.value;
  const host = rootRef.value;
  if (!svg || !host) return;

  if (strokeRef.value) {
    strokeRef.value.style.filter = `url(#${filterId})`;
  }

  const width = Math.max(
    1,
    Math.round(host.clientWidth || host.getBoundingClientRect().width || 0)
  );
  const height = Math.max(
    1,
    Math.round(host.clientHeight || host.getBoundingClientRect().height || 0)
  );

  const dyAnims = Array.from(
    svg.querySelectorAll('feOffset > animate[attributeName="dy"]')
  ) as SVGAnimateElement[];

  if (dyAnims.length >= 2) {
    dyAnims[0].setAttribute("values", `${height}; 0`);
    dyAnims[1].setAttribute("values", `0; -${height}`);
  }

  const dxAnims = Array.from(
    svg.querySelectorAll('feOffset > animate[attributeName="dx"]')
  ) as SVGAnimateElement[];

  if (dxAnims.length >= 2) {
    dxAnims[0].setAttribute("values", `${width}; 0`);
    dxAnims[1].setAttribute("values", `0; -${width}`);
  }

  // ✅ lebih ringan
  const baseDur = 10;
  const dur = Math.max(0.001, baseDur / (props.speed || 1));

  [...dyAnims, ...dxAnims].forEach(a =>
    a.setAttribute("dur", `${dur}s`)
  );

  const disp = svg.querySelector("feDisplacementMap");
  if (disp) disp.setAttribute("scale", String(10 * (props.chaos || 1)));

  const filterEl = svg.querySelector<SVGFilterElement>(
    `#${CSS.escape(filterId)}`
  );

  if (filterEl) {
    filterEl.setAttribute("x", "-200%");
    filterEl.setAttribute("y", "-200%");
    filterEl.setAttribute("width", "500%");
    filterEl.setAttribute("height", "500%");
  }

  requestAnimationFrame(() => {
    [...dyAnims, ...dxAnims].forEach((a: SVGAnimateElement) => {
      if (typeof a.beginElement === "function") {
        try {
          a.beginElement();
        } catch {}
      }
    });
  });
};

watch(
  () => [props.speed, props.chaos],
  () => updateAnim(),
  { deep: true }
);

let ro: ResizeObserver | null = null;

onMounted(() => {
  if (!rootRef.value || isMobile.value) return;
  ro = new ResizeObserver(() => updateAnim());
  ro.observe(rootRef.value);
  updateAnim();
});

onBeforeUnmount(() => {
  if (ro) ro.disconnect();
});

// ==========================
// STYLE
// ==========================
const inheritRadius = computed<CSSProperties>(() => {
  const radius = props.style?.borderRadius;

  if (radius === undefined) return { borderRadius: "inherit" };
  if (typeof radius === "number")
    return { borderRadius: `${radius}px` };

  return { borderRadius: radius };
});

const strokeStyle = computed<CSSProperties>(() => ({
  ...inheritRadius.value,
  borderWidth: `${props.thickness}px`,
  borderStyle: "solid",
  borderColor: props.color
}));

const glow1Style = computed<CSSProperties>(() => ({
  ...inheritRadius.value,
  borderWidth: `${props.thickness}px`,
  borderStyle: "solid",
  borderColor: hexToRgba(props.color, 0.6),
  filter: `blur(${1}px)`,
  opacity: 0.5
}));

const bgGlowStyle = computed<CSSProperties>(() => ({
  ...inheritRadius.value,
  transform: "scale(1.05)",
  filter: "blur(20px)",
  opacity: 0.3,
  zIndex: -1,
  background: `linear-gradient(-30deg, ${hexToRgba(
    props.color,
    0.8
  )}, transparent, ${props.color})`
}));
</script>

<template>
  <div ref="rootRef" :class="['relative isolate', className]" :style="style">

    <!-- ✅ MOBILE VERSION -->
    <div v-if="isMobile" class="absolute inset-0 pointer-events-none" :style="inheritRadius">
      <div
        class="absolute inset-0"
        :style="{
          ...inheritRadius,
          border: `${props.thickness}px solid ${props.color}`,
          boxShadow: `0 0 10px ${props.color}, 0 0 20px ${props.color}`
        }"
      />
    </div>

    <!-- ⚡ DESKTOP VERSION -->
    <template v-else>
      <svg
        ref="svgRef"
        class="fixed opacity-0 w-0 h-0 pointer-events-none"
        style="position: absolute; top: -9999px; left: -9999px"
      >
        <defs>
          <filter
            :id="filterId"
            color-interpolation-filters="sRGB"
            x="-200%"
            y="-200%"
            width="500%"
            height="500%"
          >
            <!-- ✅ lebih ringan -->
            <feTurbulence type="turbulence" baseFrequency="0.03" numOctaves="2" result="noise1" seed="1" />
            <feOffset in="noise1" dx="0" dy="0" result="offsetNoise1">
              <animate attributeName="dy" values="500; 0" dur="10s" repeatCount="indefinite" />
            </feOffset>

            <feTurbulence type="turbulence" baseFrequency="0.03" numOctaves="2" result="noise2" seed="3" />
            <feOffset in="noise2" dx="0" dy="0" result="offsetNoise2">
              <animate attributeName="dy" values="0; -500" dur="10s" repeatCount="indefinite" />
            </feOffset>

            <feComposite in="offsetNoise1" in2="offsetNoise2" operator="add" result="combinedNoise" />

            <feDisplacementMap
              in="SourceGraphic"
              in2="combinedNoise"
              scale="10"
              xChannelSelector="R"
              yChannelSelector="G"
            />
          </filter>
        </defs>
      </svg>

      <div class="absolute inset-0 pointer-events-none" :style="inheritRadius">
        <div ref="strokeRef" class="box-border absolute inset-0" :style="strokeStyle" />
        <div class="box-border absolute inset-0" :style="glow1Style" />
        <div class="absolute inset-0" :style="bgGlowStyle" />
      </div>
    </template>

    <!-- CONTENT -->
    <div class="relative" :style="inheritRadius">
      <slot />
    </div>
  </div>
</template>