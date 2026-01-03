<script lang="ts">
import Icon from "@iconify/svelte";
import { url } from "@utils/url-utils.ts";
import { onMount } from "svelte";
import DockSearch from "./DockSearch.svelte";

let props = $props();

// Configurable options - can be customized based on site needs
const config = {
	scrollThreshold: 150, // Show dock after scrolling this many pixels
	homePath: "/",
	archivePath: "/archive/",
	aboutPath: "/about/",
};

let showDock = $state(false);
let scrollTimer: ReturnType<typeof setTimeout> | null = null;

onMount(() => {
	handleScroll();

	window.addEventListener("scroll", handleScroll, { passive: true });

	return () => {
		window.removeEventListener("scroll", handleScroll);
		if (scrollTimer) {
			clearTimeout(scrollTimer);
		}
	};
});

function handleScroll() {
	if (scrollTimer) {
		clearTimeout(scrollTimer);
	}

	scrollTimer = setTimeout(() => {
		const currentScrollY = window.scrollY;
		// Dock displayed when the currentScrollY > scrollThreshold
		showDock = currentScrollY > config.scrollThreshold;
		scrollTimer = null;
	}, 16);
}

function navigateHome(event: Event) {
	event.preventDefault();
	if (window.swup) {
		window.swup.navigate(url(config.homePath));
	}
}

// Return to Top
function scrollToTop(e: Event) {
	e.stopPropagation();
	window.scrollTo({
		top: 0,
		behavior: "smooth",
	});
}

// Navigate to Archive
function navigateToArchive(event: Event) {
	event.preventDefault();
	if (window.swup) {
		window.swup.navigate(url(config.archivePath));
	}
}

// Navigate to About
function navigateToAbout(event: Event) {
	event.preventDefault();
	if (window.swup) {
		window.swup.navigate(url(config.aboutPath));
	}
}
</script>

<!-- Dock -->
<div
  id="dock"
  role="toolbar"
  tabindex="0"
  class="fixed left-1/2 z-50 transition-all duration-300 ease-out"
  class:bottom-6={showDock}
  class:-bottom-14={!showDock}
  class:opacity-100={showDock}
  class:h-18={showDock}
  class:scale-100={showDock}
>
  <!-- Backdrop Blur -->
  <div
    class="absolute inset-0 bg-white/60 dark:bg-neutral-500/60 backdrop-blur-xs rounded-full shadow-lg border border-black/10 dark:border-white/20"
  ></div>

  <!-- Buttons Container -->
  <div
    class="relative flex items-center justify-center h-full px-4 will-change-transform"
  >
    <!-- Search Button -->
    <DockSearch />

    <!-- Home Button -->
    <a
      href={url(config.homePath)}
      class="btn-plain scale-animation rounded-3xl w-11 h-11 active:scale-90"
      aria-label="Home Page"
      onclick={navigateHome}
    >
      <Icon
        icon="material-symbols:home-outline-rounded"
        class="text-[1.5rem]"
      />
    </a>

    <!-- Return to Top Button -->
    <button
      class="btn-dock-primary items-center justify-center mx-1"
      onclick={scrollToTop}
      aria-label="Return to Top"
    >
      <Icon
        icon="material-symbols:keyboard-arrow-up-rounded"
        class="text-[1.5rem]"
      />
    </button>

    <!-- Archive Button -->
    <a
      href={url(config.archivePath)}
      class="btn-plain scale-animation rounded-3xl w-11 h-11 active:scale-90"
      aria-label="Archive Page"
      onclick={navigateToArchive}
    >
      <Icon
        icon="material-symbols:inventory-2-outline-rounded"
        class="text-[1.5rem]"
      />
    </a>

    <!-- About Button -->
    <a
      href={url(config.aboutPath)}
      class="btn-plain scale-animation rounded-3xl w-11 h-11 active:scale-90"
      aria-label="About Page"
      onclick={navigateToAbout}
    >
      <Icon
        icon="material-symbols:info-outline-rounded"
        class="text-[1.5rem]"
      />
    </a>
  </div>
</div>

<style>
  /* Dock Container Style */
  #dock {
    transform: translateX(-50%);
  }

  /* Dock Main Button (Return to Top) Style */
  .btn-dock-primary {
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: var(--primary);
    color: white;
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
    transition-property: all;
    transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
    transition-duration: 200ms;
  }

  .btn-dock-primary:hover {
    opacity: 0.8;
    transform: scale(1.05);
  }
</style>