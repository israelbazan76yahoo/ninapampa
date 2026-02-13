<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import logo from '../assets/nina-pampa-logo.png';
import titulo from '../assets/nina-pampa-titulo-transp2.png';
import machupichu from '../assets/nina-pampa-machupichu.png';
import totebag from '../assets/nina-pampa-totebag.png';
import taza from '../assets/nina-pampa-taza.png';
import stickers from '../assets/nina-pampa-stickers.png';
import polo from '../assets/nina-pampa-polo.png';

// Datos de los productos
const whatsappNumber = ref('51900000000');
const selectedProduct = ref(null);
const machuPicchuImg = ref(null);
const parallaxY = ref(0);
const currentYear = new Date().getFullYear();

let ticking = false;
const updateParallax = () => {
  if (machuPicchuImg.value) {
    const speed = 0.08; // Ajusta la intensidad del efecto (menor es más sutil)
    const rect = machuPicchuImg.value.getBoundingClientRect();
    const windowHeight = window.innerHeight;
    
    if (rect.top < windowHeight && rect.bottom > 0) {
      const distanceFromCenter = (windowHeight / 2) - (rect.top + rect.height / 2);
      parallaxY.value = distanceFromCenter * speed;
    }
  }
  ticking = false;
};

const onScroll = () => {
  if (!ticking) {
    window.requestAnimationFrame(updateParallax);
    ticking = true;
  }
};

const products = ref([
  {
    id: 1,
    name: "Muña y Eucalipto",
    benefit: "Claridad Mental",
    description: "El aroma fresco de los Andes. Despeja la mente y abre las vías respiratorias para una conexión pura.",
    color: "bg-[#fdfbf7] text-emerald-800 border-emerald-800/40",
    icon: "🌿",
    details: {
      intro: "Una sinergia refrescante que evoca el aire puro de las alturas andinas.",
      comp1_title: "Muña (Minthostachys mollis)",
      comp1_desc: "Conocida como la menta de los Andes, posee propiedades vigorizantes que disipan el cansancio mental y agudizan los sentidos.",
      comp2_title: "Eucalipto",
      comp2_desc: "Poderoso purificador del aire. Su aroma alcanforado abre las vías respiratorias, facilitando la oxigenación y la claridad de pensamiento."
    }
  },
  {
    id: 2,
    name: "Salvia Blanca y Romero",
    benefit: "Limpieza Energética",
    description: "Purifica tu espacio sagrado. Una mezcla ancestral para alejar vibraciones pesadas.",
    color: "bg-[#fdfbf7] text-stone-800 border-stone-800/40",
    icon: "✨",
    details: {
      intro: "La combinación clásica para el 'sahumado' y la limpieza profunda de espacios.",
      comp1_title: "Salvia Blanca",
      comp1_desc: "Utilizada ancestralmente en ceremonias para limpiar el aura y liberar energías estancadas o negativas del ambiente.",
      comp2_title: "Romero",
      comp2_desc: "Planta solar que aporta protección y claridad. Se dice que despierta la memoria del alma y atrae alegría al hogar."
    }
  },
  {
    id: 3,
    name: "Copal y Lavanda",
    benefit: "Relajación Profunda",
    description: "La resina sagrada se une a la calma floral para inducir estados meditativos profundos.",
    color: "bg-[#fdfbf7] text-purple-900 border-purple-900/40",
    icon: "🧘",
    details: {
      intro: "Un puente entre la tierra y el cielo, ideal para la meditación y el descanso.",
      comp1_title: "Copal",
      comp1_desc: "Resina sagrada de uso ritual en América. Conecta el mundo físico con el espiritual y eleva la vibración del espacio.",
      comp2_title: "Lavanda",
      comp2_desc: "La flor de la calma por excelencia. Suaviza las emociones intensas, reduce el estrés y promueve un sueño reparador."
    }
  },
  {
    id: 4,
    name: "Cedro y Canela",
    benefit: "Prosperidad",
    description: "Madera noble y especias cálidas para atraer abundancia y calidez al hogar.",
    color: "bg-[#fdfbf7] text-orange-900 border-orange-900/40",
    icon: "🔥",
    details: {
      intro: "Un aroma cálido y envolvente que invita a la seguridad y la abundancia.",
      comp1_title: "Cedro",
      comp1_desc: "Madera noble que aporta fortaleza, estabilidad y arraigo. Ayuda a concretar proyectos y limpiar espacios nuevos.",
      comp2_title: "Canela",
      comp2_desc: "Especia estimulante regida por el sol. Atrae la buena fortuna, el éxito y calienta el corazón, elevando el ánimo."
    }
  },
  {
    id: 5,
    name: "Palo Santo y Rosas",
    benefit: "Amor y Apertura",
    description: "La madera sagrada suavizada por la dulzura de las rosas para abrir el chakra corazón.",
    color: "bg-[#fdfbf7] text-rose-900 border-rose-900/40",
    icon: "🌹",
    details: {
      intro: "Una caricia aromática para el alma, fomentando el amor propio y la armonía.",
      comp1_title: "Palo Santo",
      comp1_desc: "Madera sagrada que limpia energéticamente con dulzura, atrayendo energías benévolas y buena suerte.",
      comp2_title: "Rosas",
      comp2_desc: "Símbolo universal del amor. Su vibración alta abre el chakra corazón, suaviza conflictos y aporta armonía emocional."
    }
  }
]);

const benefits = ref([
  {
    id: 1,
    title: "100% Natural",
    description: "Sin carbón, sin químicos. Solo plantas, resinas y madera del Valle Sagrado.",
    icon: '<path d="M12 22c0-6-4-12-4-12s2-6 4-6 4 6 4 6-4 12z" /><path d="M12 4v14" />'
  },
  {
    id: 2,
    title: "Aromaterapia",
    description: "Fragancias sutiles que calman la mente y purifican el ambiente.",
    icon: '<path d="M6 5c2 2 2 4 0 6s-2 4 0 6" /><path d="M12 3c2 2 2 4 0 6s-2 4 0 6" /><path d="M18 5c2 2 2 4 0 6s-2 4 0 6" />'
  },
  {
    id: 3,
    title: "Energía Viva",
    description: "Hechos a mano con intención y respeto por los ciclos de la naturaleza.",
    icon: '<circle cx="12" cy="12" r="4" /><path d="M12 2v2" /><path d="M12 20v2" /><path d="M4.93 4.93l1.41 1.41" /><path d="M17.66 17.66l1.41 1.41" /><path d="M2 12h2" /><path d="M20 12h2" /><path d="M6.34 17.66l-1.41 1.41" /><path d="M19.07 4.93l-1.41 1.41" />'
  }
]);

const promotions = ref([
  {
    id: 1,
    title: "Pack Místico",
    description: "Lleva 3 cajas de incienso y recibe un set de stickers de regalo.",
    condition: "Compra 3 cajas",
    gift: "Stickers de Regalo",
    icon: "🎁"
  },
  {
    id: 2,
    title: "Pack Ancestral",
    description: "Por compras superiores a S/100, llévate un Tote Bag exclusivo de Nina Pampa.",
    condition: "Compras > S/100",
    gift: "Tote Bag Gratis",
    icon: "👜"
  }
]);

const merchItems = ref([
  { id: 1, name: "Tote Bag Nina Pampa", price: "S/ 35.00", image: totebag, description: "Lleva la magia contigo. Algodón 100% orgánico." },
  { id: 2, name: "Taza Ceremonial", price: "S/ 25.00", image: taza, description: "Para tus infusiones sagradas. Cerámica artesanal." },
  { id: 3, name: "Polo Espíritu Andino", price: "S/ 45.00", image: polo, description: "Diseños inspirados en la cosmovisión andina." },
  { id: 4, name: "Set de Stickers", price: "S/ 10.00", image: stickers, description: "Decora tu espacio con nuestros símbolos sagrados." }
]);

const scrollToPromos = () => {
  document.getElementById('promociones').scrollIntoView({ behavior: 'smooth' });
};

const scrollToMerch = () => {
  document.getElementById('merchandising').scrollIntoView({ behavior: 'smooth' });
};

const scrollToProducts = () => {
  document.getElementById('productos').scrollIntoView({ behavior: 'smooth' });
};

const scrollToPoints = () => {
  document.getElementById('puntos-venta').scrollIntoView({ behavior: 'smooth' });
};

const scrollToEssence = () => {
  document.getElementById('nuestra-historia').scrollIntoView({ behavior: 'smooth' });
};

const openDetails = (product) => {
  selectedProduct.value = product;
};

const closeDetails = () => {
  selectedProduct.value = null;
};

const faqs = ref([
  {
    question: "¿De qué están hechos sus inciensos?",
    answer: "Nuestros inciensos son 100% naturales, elaborados a mano con plantas medicinales, resinas y maderas recolectadas sosteniblemente en el Valle Sagrado de los Incas. No utilizamos carbón, químicos ni fragancias sintéticas."
  },
  {
    question: "¿Cuánto tiempo dura cada varita?",
    answer: "Debido a su alta concentración de materia prima natural, cada varita tiene una duración aproximada de 45 a 60 minutos, dependiendo de la ventilación del ambiente."
  },
  {
    question: "¿Cómo debo encender el incienso?",
    answer: "Enciende la punta de la varita con un fósforo o encendedor, deja que la llama arda unos segundos hasta que se forme una brasa roja y luego sóplala suavemente. Colócalo en un portaincienso seguro."
  },
  {
    question: "¿Realizan envíos a todo el Perú?",
    answer: "Sí, realizamos envíos a nivel nacional a través de agencias de confianza como Shalom u Olva Courier. El tiempo de entrega varía según el destino (usualmente 2-4 días hábiles)."
  },
  {
    question: "¿Tienen precios al por mayor?",
    answer: "¡Claro que sí! Ofrecemos precios especiales para mayoristas, tiendas holísticas y distribuidores. Contáctanos por WhatsApp para enviarte nuestro catálogo mayorista."
  }
]);

const activeFaq = ref(null);

const toggleFaq = (index) => {
  activeFaq.value = activeFaq.value === index ? null : index;
};

onMounted(() => {
  window.addEventListener('scroll', onScroll);
  updateParallax();
});

onUnmounted(() => {
  window.removeEventListener('scroll', onScroll);
});
</script>

<template>
  <div class="min-h-screen bg-stone-50 font-cormorant text-stone-900 font-medium overflow-x-hidden animate-fade-in-page text-lg">
    
    <!-- Navbar Flotante -->
    <nav class="fixed w-full z-50 bg-white/80 backdrop-blur-md border-b border-stone-200">
      <div class="container mx-auto px-6 py-4 flex justify-between items-center">
        <div class="flex items-end gap-4">
          <img :src="logo" alt="Logo Nina Pampa" class="w-24 h-24 object-contain" />
          <div class="text-center hidden md:block">
            <img :src="titulo" alt="Nina Pampa" class="h-28 object-contain" loading="lazy" />
          </div>
        </div>
        <div class="flex flex-col-reverse md:flex-row items-center gap-2 md:gap-6">
          <button @click="scrollToPoints" class="text-stone-800 hover:text-orange-700 font-cinzel font-bold text-xs md:text-sm transition-colors">
            Puntos de Venta
          </button>
          <a :href="`https://wa.me/${whatsappNumber}`" target="_blank" class="bg-orange-700 hover:bg-orange-800 text-white px-5 py-2 rounded-full text-sm font-cinzel font-bold transition-all duration-300 shadow-md hover:shadow-lg flex items-center gap-2">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-5 h-5"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
            Contáctenos
          </a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <header class="relative min-h-screen flex items-center justify-center overflow-hidden bg-[#fdfbf7] pt-24 pb-32">
      <!-- Fondo dibujado a mano (SVG) -->
      <div class="absolute inset-0 z-0 overflow-hidden pointer-events-none">
        <!-- Sol -->
        <svg class="absolute top-10 right-10 md:top-20 md:right-20 w-32 h-32 md:w-64 md:h-64 text-orange-200/50 animate-pendulum" viewBox="0 0 200 200" fill="currentColor">
          <path d="M100 20 C 150 20 180 50 180 100 C 180 150 150 180 100 180 C 50 180 20 150 20 100 C 20 50 50 20 100 20 Z" />
        </svg>

        <!-- Nubes -->
        <svg class="absolute top-1/2 left-10 w-64 h-32 text-stone-300 animate-drift" viewBox="0 0 100 50" fill="currentColor">
           <path d="M10 30 Q 30 5 50 30 T 90 30 Q 100 45 80 45 H 20 Q 0 45 10 30 Z" />
        </svg>
        <svg class="absolute top-2/3 right-1/4 w-96 h-48 text-stone-300/80 animate-drift-delayed" viewBox="0 0 100 50" fill="currentColor">
           <path d="M10 30 Q 30 5 50 30 T 90 30 Q 100 45 80 45 H 20 Q 0 45 10 30 Z" />
        </svg>

        <!-- Montañas -->
        <svg class="absolute bottom-0 left-0 w-full h-full text-stone-200/60" preserveAspectRatio="none" viewBox="0 0 1200 600" fill="currentColor">
          <path d="M0 600 L0 300 Q 150 100 300 300 T 600 250 T 900 350 T 1200 200 V 600 Z" />
        </svg>
        <svg class="absolute bottom-0 left-0 w-full h-2/3 text-stone-300/60" preserveAspectRatio="none" viewBox="0 0 1200 400" fill="currentColor">
          <path d="M0 400 L0 200 Q 200 50 400 200 T 800 150 T 1200 250 V 400 Z" />
        </svg>

        <!-- Rio -->
        <svg class="absolute bottom-0 w-full h-1/3 text-blue-200/20" preserveAspectRatio="none" viewBox="0 0 1200 200" fill="none" stroke="currentColor" stroke-width="40" stroke-linecap="round">
           <path d="M-100 200 Q 300 0 600 100 T 1300 50" />
        </svg>
      </div>

      <div class="relative z-10 text-center px-4 max-w-4xl mx-auto">
        <div class="flex justify-center mb-2 animate-fade-in-up delay-100">
          <img :src="titulo" alt="Nina Pampa" class="h-56 md:h-96 object-contain" fetchpriority="high" />
        </div>
        <p class="text-xl md:text-2xl text-stone-900 mb-10 font-medium max-w-2xl mx-auto animate-fade-in-up delay-200">
          Inciensos artesanales creados con la energía mística del Valle Sagrado de Urubamba, Cusco. 
          Conecta con la naturaleza a través del fuego sagrado de Nina Pampa.
        </p>
        <div class="flex flex-wrap gap-4 justify-center animate-fade-in-up delay-300 max-w-3xl mx-auto">
          <button @click="scrollToProducts" class="px-8 py-4 bg-orange-600 hover:bg-orange-700 text-white rounded-full font-cinzel font-bold transition-all hover:scale-105 shadow-xl hover:shadow-orange-900/20">
            Descubrir Aromas
          </button>
          <button @click="scrollToEssence" class="px-8 py-4 bg-transparent hover:bg-stone-100 text-stone-700 border border-stone-300 rounded-full font-cinzel font-bold transition-all hover:scale-105">
            Nuestra Historia
          </button>
          <button @click="scrollToPromos" class="px-8 py-4 bg-emerald-700 hover:bg-emerald-800 text-white rounded-full font-cinzel font-bold transition-all hover:scale-105 shadow-xl hover:shadow-emerald-900/20">
            Promociones
          </button>
          <button @click="scrollToMerch" class="px-8 py-4 bg-stone-800 hover:bg-stone-900 text-white rounded-full font-cinzel font-bold transition-all hover:scale-105 shadow-xl hover:shadow-stone-900/20">
            Merchandising
          </button>
        </div>
      </div>

      <!-- Elemento decorativo místico -->
      <div class="absolute bottom-10 left-1/2 -translate-x-1/2 animate-bounce-slow text-stone-400">
        <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 5v14"/><path d="m19 12-7 7-7-7"/></svg>
      </div>

      <!-- Animación de Incienso Flotante (Móvil - Detrás del título) -->
      <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 text-stone-400 animate-float lg:hidden pointer-events-none z-0 opacity-40">
        <svg width="220" height="352" viewBox="0 0 100 160" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round">
          <!-- Humo (Estelas animadas) -->
          <path class="animate-smoke-1 opacity-0" d="M50 60 Q 55 50 50 40 T 50 10" />
          <path class="animate-smoke-2 opacity-0" d="M42 55 Q 38 45 42 30 T 40 5" />
          <path class="animate-smoke-3 opacity-0" d="M58 55 Q 62 45 58 35 T 60 10" />
          
          <!-- Varillas -->
          <path d="M50 80 L 50 60" />
          <path d="M50 80 L 42 55" />
          <path d="M50 80 L 58 55" />
          
          <!-- Cuenco -->
          <path d="M30 80 Q 50 100 70 80" />
          <path d="M30 80 L 70 80" />
          <path d="M35 80 Q 50 90 65 80" opacity="0.5" />
        </svg>
      </div>

      <!-- Animación de Incienso Flotante (Izquierda) -->
      <div class="absolute top-1/2 -translate-y-1/2 left-10 xl:left-32 text-stone-400 animate-float hidden lg:block pointer-events-none z-0 opacity-60">
        <svg width="200" height="320" viewBox="0 0 100 160" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round">
          <!-- Humo (Estelas animadas) -->
          <path class="animate-smoke-1 opacity-0" d="M50 60 Q 55 50 50 40 T 50 10" />
          <path class="animate-smoke-2 opacity-0" d="M42 55 Q 38 45 42 30 T 40 5" />
          <path class="animate-smoke-3 opacity-0" d="M58 55 Q 62 45 58 35 T 60 10" />
          
          <!-- Varillas -->
          <path d="M50 80 L 50 60" />
          <path d="M50 80 L 42 55" />
          <path d="M50 80 L 58 55" />
          
          <!-- Cuenco -->
          <path d="M30 80 Q 50 100 70 80" />
          <path d="M30 80 L 70 80" />
          <path d="M35 80 Q 50 90 65 80" opacity="0.5" />
        </svg>
      </div>

      <!-- Animación de Incienso Flotante (Derecha) -->
      <div class="absolute top-1/2 -translate-y-1/2 right-10 xl:right-32 text-stone-400 animate-float hidden lg:block pointer-events-none z-0 opacity-60 scale-x-[-1]">
        <svg width="200" height="320" viewBox="0 0 100 160" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round">
          <!-- Humo (Estelas animadas) -->
          <path class="animate-smoke-1 opacity-0" d="M50 60 Q 55 50 50 40 T 50 10" />
          <path class="animate-smoke-2 opacity-0" d="M42 55 Q 38 45 42 30 T 40 5" />
          <path class="animate-smoke-3 opacity-0" d="M58 55 Q 62 45 58 35 T 60 10" />
          
          <!-- Varillas -->
          <path d="M50 80 L 50 60" />
          <path d="M50 80 L 42 55" />
          <path d="M50 80 L 58 55" />
          
          <!-- Cuenco -->
          <path d="M30 80 Q 50 100 70 80" />
          <path d="M30 80 L 70 80" />
          <path d="M35 80 Q 50 90 65 80" opacity="0.5" />
        </svg>
      </div>
    </header>

    <!-- Sección de Beneficios -->
    <section class="py-20 bg-[#fdfbf7] relative z-10">
      <div class="container mx-auto px-6">
        <div class="grid md:grid-cols-3 gap-12">
          <div v-for="benefit in benefits" :key="benefit.id" class="flex flex-col items-center text-center group">
            <div class="w-20 h-20 mb-6 relative flex items-center justify-center">
               <!-- Mancha de fondo estilo acuarela/dibujo -->
               <svg class="absolute inset-0 w-full h-full text-orange-100 group-hover:scale-110 transition-transform duration-500" viewBox="0 0 100 100" fill="currentColor" style="filter: drop-shadow(0px 4px 4px rgba(0,0,0,0.05));">
                  <path d="M38.3,18.6c13.4-5.6,29.3-0.6,37.6,11.4c8.3,12,8.6,28.6,0.5,39.9c-8.1,11.3-23.7,15.8-37.6,11.4 C25,76.9,15.3,64.3,14.2,49.9C13.1,35.5,24.9,24.2,38.3,18.6z" />
               </svg>
               <!-- Icono -->
               <svg class="w-10 h-10 text-orange-800 relative z-10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" v-html="benefit.icon"></svg>
            </div>
            <h3 class="text-xl font-cinzel font-bold text-stone-800 mb-3">{{ benefit.title }}</h3>
            <p class="text-stone-800 font-medium leading-relaxed">{{ benefit.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección de Origen / Misticismo -->
    <section id="nuestra-historia" class="py-24 bg-stone-50 relative">
      <div class="container mx-auto px-6">
        <div class="grid md:grid-cols-2 gap-16 items-center">
          <div class="relative group">
            <div class="absolute -inset-4 bg-orange-200 rounded-2xl rotate-2 group-hover:rotate-1 transition-transform duration-500 opacity-50"></div>
            <img 
              ref="machuPicchuImg"
              :src="machupichu" 
              alt="Incienso Artesanal" 
              class="relative rounded-xl shadow-2xl w-full object-cover object-top h-[500px] will-change-transform"
              :style="{ transform: `translateY(${parallaxY}px)` }"
              loading="lazy"
              decoding="async"
            />
            <!-- Badge Flotante -->
            <div class="absolute -bottom-6 -right-6 bg-white p-6 rounded-lg shadow-xl max-w-xs border-l-4 border-orange-600">
              <p class="text-stone-600 italic font-serif">"El fuego (Nina) transforma la materia en espíritu."</p>
            </div>
          </div>
          
          <div>
            <h2 class="text-orange-700 font-cinzel font-bold tracking-widest text-sm mb-2 uppercase">Nuestra Historia</h2>
            <h3 class="text-4xl font-cinzel font-bold text-stone-900 mb-6">Nacidos bajo el sol de Cusco</h3>
            <p class="text-stone-800 font-medium text-xl leading-relaxed mb-6">
              En el corazón del <strong>Valle de Urubamba</strong>, donde las montañas tocan el cielo, nace 
              <span class="text-orange-700 font-semibold">Nina Pampa</span>. Somos un emprendimiento dedicado a preservar 
              la sabiduría ancestral a través de los aromas.
            </p>
            <p class="text-stone-800 font-medium text-xl leading-relaxed mb-8">
              Cada varita de incienso es moldeada a mano, utilizando hierbas recolectadas con respeto a la Pachamama. 
              No solo vendemos inciensos; compartimos una herramienta para tu ritual diario, un puente hacia la calma 
              y la conexión espiritual.
            </p>
            
            <div class="grid grid-cols-2 gap-6">
              <div class="flex items-start gap-3">
                <div class="p-2 bg-stone-200 rounded-full text-stone-700">🌿</div>
                <div>
                  <h4 class="font-bold text-stone-900">100% Natural</h4>
                  <p class="text-sm text-stone-700 font-medium">Sin químicos nocivos.</p>
                </div>
              </div>
              <div class="flex items-start gap-3">
                <div class="p-2 bg-stone-200 rounded-full text-stone-700">👐</div>
                <div>
                  <h4 class="font-bold text-stone-900">Hecho a Mano</h4>
                  <p class="text-sm text-stone-700 font-medium">Artesanía local.</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Catálogo de Productos -->
    <section id="productos" class="py-24 bg-white">
      <div class="container mx-auto px-6">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-4xl font-cinzel font-bold text-stone-900 mb-4">Nuestros Aromas</h2>
          <p class="text-stone-700 font-medium">Cada aroma tiene un propósito. Encuentra el que tu alma necesita hoy.</p>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="product in products" 
            :key="product.id"
            class="group relative bg-[#e6ccb2] hover:bg-[#ebd4c0] rounded-lg p-8 border-4 border-[#9c6644] transition-all duration-300 hover:-translate-y-1 shadow-[6px_6px_0_0_#7f5539] hover:shadow-[10px_10px_0_0_#7f5539]"
          >
            <div class="absolute top-6 right-6 text-4xl opacity-20 group-hover:opacity-100 group-hover:scale-110 transition-all duration-500">
              {{ product.icon }}
            </div>
            
            <div :class="`inline-block px-4 py-1 rounded-sm text-xs font-cinzel font-bold mb-4 border-dashed border-2 shadow-sm bg-noise ${product.color}`">
              {{ product.benefit }}
            </div>
            
            <h3 class="text-2xl font-cinzel font-bold text-stone-800 mb-3 group-hover:text-orange-700 transition-colors">
              {{ product.name }}
            </h3>
            
            <p class="text-stone-800 font-medium mb-6 leading-relaxed">
              {{ product.description }}
            </p>
            
            <button @click="openDetails(product)" class="text-stone-900 font-bold text-sm border-b-2 border-[#9c6644] hover:border-stone-900 transition-all pb-1">
              Ver detalles
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección de Promociones -->
    <section id="promociones" class="py-24 bg-orange-50">
      <div class="container mx-auto px-6">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-4xl font-cinzel font-bold text-stone-900 mb-4">Promociones Especiales</h2>
          <p class="text-stone-700 font-medium">Regalos pensados para complementar tu ritual.</p>
        </div>

        <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
          <div v-for="promo in promotions" :key="promo.id" class="bg-white p-8 rounded-lg shadow-lg border-2 border-orange-200 relative overflow-hidden group hover:border-orange-400 transition-colors">
            <div class="absolute top-0 right-0 bg-orange-600 text-white px-4 py-1 rounded-bl-lg font-cinzel font-bold text-sm">Oferta</div>
            <div class="flex items-center gap-6 mb-4">
              <div class="text-5xl group-hover:scale-110 transition-transform duration-300">{{ promo.icon }}</div>
              <div>
                <h3 class="text-2xl font-cinzel font-bold text-stone-800">{{ promo.title }}</h3>
                <p class="text-orange-700 font-bold text-sm uppercase tracking-wider">{{ promo.condition }}</p>
              </div>
            </div>
            <p class="text-stone-600 font-medium mb-4">{{ promo.description }}</p>
            <div class="bg-orange-50 p-3 rounded text-center border border-orange-100">
              <span class="text-stone-800 font-bold">🎁 Regalo: {{ promo.gift }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección de Merchandising -->
    <section id="merchandising" class="py-24 bg-white">
      <div class="container mx-auto px-6">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-4xl font-cinzel font-bold text-stone-900 mb-4">Merchandising</h2>
          <p class="text-stone-700 font-medium">Lleva la esencia de Nina Pampa contigo.</p>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
          <div v-for="item in merchItems" :key="item.id" class="group text-center">
            <div class="bg-stone-100 rounded-xl p-8 mb-4 transition-all duration-300 group-hover:bg-stone-200 group-hover:shadow-lg flex items-center justify-center h-64 relative">
              <img v-if="item.image" :src="item.image" :alt="item.name" class="w-full h-full object-contain group-hover:scale-110 transition-transform duration-500" />
              <div v-else class="text-8xl opacity-80 group-hover:scale-110 transition-transform duration-500">{{ item.icon }}</div>
              <div class="absolute bottom-4 right-4 bg-white px-3 py-1 rounded-full text-sm font-bold text-stone-800 shadow-sm">{{ item.price }}</div>
            </div>
            <h3 class="text-xl font-cinzel font-bold text-stone-800 mb-2">{{ item.name }}</h3>
            <p class="text-stone-600 text-sm px-4">{{ item.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Puntos de Venta -->
    <section id="puntos-venta" class="py-24 bg-[#fdfbf7]">
      <div class="container mx-auto px-6">
        <div class="text-center max-w-3xl mx-auto mb-16">
          <h2 class="text-4xl font-cinzel font-bold text-stone-900 mb-4">Puntos de Venta</h2>
          <p class="text-stone-700 font-medium">Encuentra nuestros inciensos en los siguientes lugares del Valle Sagrado.</p>
        </div>

        <div class="grid md:grid-cols-2 gap-8 max-w-4xl mx-auto">
          <div class="bg-white p-8 rounded-lg shadow-md border-l-4 border-orange-700 hover:shadow-xl transition-shadow duration-300">
            <h3 class="text-2xl font-cinzel font-bold text-stone-800 mb-2">Mercado de Urubamba</h3>
            <p class="text-stone-600 font-medium">Puesto 45, Sección Artesanías</p>
            <p class="text-stone-500 text-sm mt-2">Lunes a Domingo, 8am - 5pm</p>
          </div>

          <div class="bg-white p-8 rounded-lg shadow-md border-l-4 border-orange-700 hover:shadow-xl transition-shadow duration-300">
            <h3 class="text-2xl font-cinzel font-bold text-stone-800 mb-2">Feria de Pisac</h3>
            <p class="text-stone-600 font-medium">Plaza de Armas</p>
            <p class="text-stone-500 text-sm mt-2">Domingos, 9am - 4pm</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Preguntas Frecuentes -->
    <section class="py-24 bg-white">
      <div class="container max-w-3xl mx-auto px-6">
        <div class="text-center mb-16">
          <h2 class="text-4xl font-cinzel font-bold text-stone-900 mb-4">Preguntas Frecuentes</h2>
          <p class="text-stone-700 font-medium">Resolvemos tus dudas sobre nuestros productos artesanales.</p>
        </div>

        <div class="space-y-4">
          <div 
            v-for="(faq, index) in faqs" 
            :key="index"
            class="border-2 border-[#9c6644]/20 rounded-lg overflow-hidden transition-all duration-300 hover:border-[#9c6644]/50"
          >
            <button 
              @click="toggleFaq(index)"
              class="w-full flex items-center justify-between p-6 text-left bg-[#fdfbf7] hover:bg-orange-50 transition-colors"
            >
              <span class="font-cinzel font-bold text-stone-800 text-lg">{{ faq.question }}</span>
              <span class="text-orange-700 text-2xl transition-transform duration-300" :class="{'rotate-180': activeFaq === index}">
                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m6 9 6 6 6-6"/></svg>
              </span>
            </button>
            <div 
              class="grid transition-all duration-300 ease-in-out"
              :class="activeFaq === index ? 'grid-rows-[1fr] opacity-100' : 'grid-rows-[0fr] opacity-0'"
            >
              <div class="overflow-hidden">
                <div class="bg-white p-6 text-stone-700 font-medium border-t-2 border-[#9c6644]/10">
                  <p class="leading-relaxed">{{ faq.answer }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-orange-50 text-stone-900 py-8">
      <div class="container mx-auto px-6">
        <div class="flex flex-col md:flex-row justify-between items-center gap-8">
          <div class="text-center md:text-left">
            <div class="flex items-center justify-center md:justify-start gap-3 mb-2">
              <img :src="logo" alt="Logo Nina Pampa" class="w-20 h-20 object-contain" loading="lazy" decoding="async" />
              <img :src="titulo" alt="Nina Pampa" class="h-20 object-contain" loading="lazy" decoding="async" />
            </div>
            <p>Valle de Urubamba, Cusco - Perú.</p>
          </div>
          <div class="flex gap-6">
            <a href="#" class="group relative hover:text-orange-500 transition-colors" aria-label="Instagram">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6"><rect width="20" height="20" x="2" y="2" rx="5" ry="5"/><path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"/><line x1="17.5" x2="17.51" y1="6.5" y2="6.5"/></svg>
              <span class="absolute -top-10 left-1/2 -translate-x-1/2 bg-white text-stone-700 text-xs font-cinzel px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity duration-300 pointer-events-none whitespace-nowrap border border-stone-200 shadow-lg">Instagram</span>
            </a>
            <a href="#" class="group relative hover:text-orange-500 transition-colors" aria-label="Facebook">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6"><path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/></svg>
              <span class="absolute -top-10 left-1/2 -translate-x-1/2 bg-white text-stone-700 text-xs font-cinzel px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity duration-300 pointer-events-none whitespace-nowrap border border-stone-200 shadow-lg">Facebook</span>
            </a>
            <a :href="`https://wa.me/${whatsappNumber}`" target="_blank" class="group relative hover:text-orange-500 transition-colors" aria-label="WhatsApp">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="w-6 h-6"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
              <span class="absolute -top-10 left-1/2 -translate-x-1/2 bg-white text-stone-700 text-xs font-cinzel px-2 py-1 rounded opacity-0 group-hover:opacity-100 transition-opacity duration-300 pointer-events-none whitespace-nowrap border border-stone-200 shadow-lg">WhatsApp</span>
            </a>
          </div>
        </div>
        <div class="border-t border-stone-200 mt-12 pt-8 text-center text-sm">
          <p>&copy; {{ currentYear }} Nina Pampa. Todos los derechos reservados.</p>
        </div>
      </div>
    </footer>

    <!-- Modal de Detalles -->
    <div v-if="selectedProduct" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-stone-900/60 backdrop-blur-sm transition-opacity animate-fade-in-page" @click.self="closeDetails">
      <div class="bg-[#fdfbf7] rounded-lg shadow-2xl max-w-lg w-full p-8 relative border-4 border-[#9c6644] animate-fade-in-up overflow-y-auto max-h-[90vh]">
          <button @click="closeDetails" class="absolute top-4 right-4 text-stone-500 hover:text-orange-700 transition-colors">
            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"></line><line x1="6" y1="6" x2="18" y2="18"></line></svg>
          </button>
          
          <div class="text-center mb-6">
              <div class="text-6xl mb-4 animate-bounce-slow">{{ selectedProduct.icon }}</div>
              <h3 class="text-3xl font-cinzel font-bold text-stone-900">{{ selectedProduct.name }}</h3>
              <p class="text-orange-700 font-cinzel font-bold mt-2 tracking-wide">{{ selectedProduct.benefit }}</p>
          </div>
          
          <div class="space-y-6 text-stone-700 font-medium">
              <p class="italic text-center text-lg">{{ selectedProduct.details.intro }}</p>
              
              <div class="bg-orange-50/50 p-4 rounded border border-orange-100/50">
                  <h4 class="font-cinzel font-bold text-orange-900 mb-1 text-lg">{{ selectedProduct.details.comp1_title }}</h4>
                  <p class="text-sm leading-relaxed">{{ selectedProduct.details.comp1_desc }}</p>
              </div>
              
              <div class="bg-stone-100/50 p-4 rounded border border-stone-200/50">
                  <h4 class="font-cinzel font-bold text-stone-800 mb-1 text-lg">{{ selectedProduct.details.comp2_title }}</h4>
                  <p class="text-sm leading-relaxed">{{ selectedProduct.details.comp2_desc }}</p>
              </div>
          </div>
          
          <!--div class="mt-8 text-center">
               <a :href="`https://wa.me/${whatsappNumber}?text=Hola Nina Pampa, me interesa el incienso de ${selectedProduct.name}`" target="_blank" class="inline-flex items-center gap-2 bg-orange-700 hover:bg-orange-800 text-white px-8 py-3 rounded-full font-cinzel font-bold transition-all shadow-md hover:shadow-lg hover:-translate-y-1">
                  <span>Pedir este aroma</span>
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/></svg>
              </a>
          </div-->
      </div>
    </div>
  </div>
</template>

<style scoped>
.animate-fade-in-up {
  animation: fadeInUp 1s ease-out forwards;
}
.delay-100 { animation-delay: 0.1s; }
.delay-200 { animation-delay: 0.2s; }
.delay-300 { animation-delay: 0.3s; }

@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.animate-bounce-slow {
  animation: bounce 3s infinite;
}

.animate-pulse-slow {
  animation: pulse 6s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

.animate-drift {
  animation: drift 60s linear infinite;
}
.animate-drift-delayed {
  animation: drift 85s linear infinite;
  animation-delay: -30s;
}

@keyframes drift {
  from { transform: translateX(-120vw); }
  to { transform: translateX(120vw); }
}

.animate-fade-in-page {
  animation: fadeInPage 1.5s ease-out forwards;
}

@keyframes fadeInPage {
  from { opacity: 0; }
  to { opacity: 1; }
}

.bg-noise {
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)' opacity='0.08'/%3E%3C/svg%3E");
}

/* Animaciones para el incienso */
.animate-float {
  animation: float 6s ease-in-out infinite;
}
@keyframes float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-10px); }
}
.animate-smoke-1 { animation: smoke 4s ease-out infinite; }
.animate-smoke-2 { animation: smoke 5s ease-out infinite 1s; }
.animate-smoke-3 { animation: smoke 4.5s ease-out infinite 2s; }
@keyframes smoke {
  0% { opacity: 0; transform: translateY(0); }
  30% { opacity: 0.6; }
  100% { opacity: 0; transform: translateY(-30px); }
}

/* Animación pendular para el sol */
.animate-pendulum {
  animation: pendulum 12s ease-in-out infinite;
  transform-origin: 50% -50%;
}
@keyframes pendulum {
  0%, 100% { transform: rotate(-8deg); }
  50% { transform: rotate(8deg); }
}
</style>