<!-- src/routes/index.svelte -->
<script>
  import '../routes/global.css';
  import './__layout.svelte';

  let imageClass = "sm:w-28 md:w-32 lg:w-40 xl:w-48 h-full sm:h-28 md:h-32 lg:h-40 xl:h-48 object-cover rounded-lg";
  let textClass = "text-center text-blue-500 hover:underline";

  //Carousel
  import { onMount } from "svelte";

  let slideIndex = 0;

  onMount(() => {
    showSlides();
  });

  function showSlides() {
    if (typeof document === "undefined") {
      // Running on the server, do nothing
      return;
    }

    let slides = document.querySelectorAll(".mySlides");
    let dots = document.querySelectorAll(".dot");

    for (let i = 0; i < slides.length; i++) {
      slides[i].style.display = "none";
    }

    slideIndex++;
    if (slideIndex > slides.length) slideIndex = 1;

    for (let i = 0; i < dots.length; i++) {
      dots[i].classList.remove("active");
    }

    slides[slideIndex - 1].style.display = "block";
    slides[slideIndex - 1].classList.add("slide-in");
    dots[slideIndex - 1].classList.add("active");

    setTimeout(showSlides, 5000); // Change image every 2 seconds
  }

  // FAQ
  // Object to track FAQ dropdown states
let faqDropdowns = {};

// Function to toggle the state of a specific FAQ dropdown
function toggleAnswer(id) {
  faqDropdowns = {
    ...faqDropdowns,
    [id]: !faqDropdowns[id],
  };
}

// Function to handle clicks outside FAQ dropdowns
function handleClickOutside(event) {
  for (const id in faqDropdowns) {
    // Check if the dropdown is open and the clicked element is outside of it
    if (faqDropdowns[id] && !event.target.closest(`.${id}`)) {
      // Close the dropdown by updating the state
      faqDropdowns = {
        ...faqDropdowns,
        [id]: false,
      };
    }
  }
}

  //Dropdown for products
  let ImgDropdowns = {};

  function toggleDrop(id) {
    // Close other dropdowns when opening a new one
    Object.keys(ImgDropdowns).forEach((key) => {
      if (key !== id) {
        ImgDropdowns[key] = false;
      }
    });

    ImgDropdowns = {
      ...ImgDropdowns,
      [id]: !ImgDropdowns[id],
    };
  }

  function ClickOutside(event, id) {
    if (ImgDropdowns[id] && !event.target.closest(`.${id}`)) {
      ImgDropdowns = {
        ...ImgDropdowns,
        [id]: false,
      };
    }
  }
</script>

<style>
  * {box-sizing: border-box;}
  body {font-family: Verdana, sans-serif;}
  .mySlides {display: none;}
  img {vertical-align:middle;}
  
  /* Slideshow container */
  .slideshow-container {
    max-width: 80%;
    padding: 10px;
    position: relative;
    margin: 10px;
  }
  
  .active {
    background-color: #717171;
  }
  
  /* Sliding animation */
  .slide-in {
    animation-name: slideIn;
    animation-duration: 1s;
  }
  
  @keyframes slideIn {
    from {
      transform: translateX(100%);
    }
    to {
      transform: translateX(0);
    }
  }
  
  /* On smaller screens, decrease text size */
  @media only screen and (max-width: 400px) {
    .text {font-size: 11px}
  }
  /* FAQ */
  .faq-container {
    max-width: 80%;
    margin: auto;
  }

  .question {
    cursor: pointer;
    background-color: #216150;
    color: white;
    padding: 16px;
    font-size: 16px;
    border: 1px solid white;
  }

  .answer {
    border: 1px solid white;
    display: none;
    padding: 12px 16px;
    background-color: #216157;
    width: 100%;
    margin: 0;
  }

  .question:hover,
  .question:focus {
    background-color: #1e796b;
  }

  .question.active {
    background-color: #216150;
  }

  .answer.active {
    display: block;
  }

  /* dropdown */
  /* Styling for the dropdown container */
  .dropdown-container {
    position: relative;
    display: inline-block;
    width: auto;
    background: none;
  }

  /* Styling for the dropdown content */
  .dropdown-content {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    width: 90% !important;
    background-color: #fff;
    border: 1px solid #ccc;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
    z-index: 1;
  }

  /* Styling for the dropdown links */
  .dropdown-content a {
    display: block;
    padding: 10px;
    text-decoration: none;
  }

  .dropdown-button {
    background: none;
    border: none;
    padding: 0;
    font: inherit;
    cursor: pointer;
    text-align: left;
    outline: none;
  }

  /* Show the dropdown content when hovering over the dropdown container */
  .dropdown-container.active .dropdown-content {
    display: block;
  }
  </style>


<div class="bg-gray-800 pt-3 pb-3 pl-5 pr-10">
  <!-- Tailwind CSS styling for the navbar -->
  <nav class="flex justify-self-start items-center">
    <!-- Home link (redirects to the same page) -->
    <a href="#home" class="mr-4">
      <!-- Example of an inline SVG for a simple home icon -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
        class="h-6 w-6 text-white"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"
        />
      </svg>
    </a>

    <a href="#home" class="text-white">Home</a>

    <!-- Products -->
    <a href="#products" class="text-white ml-7">Products</a>

    <!-- About Us -->
    <a href="#about" class="text-white ml-7">About Us</a>

    <!-- Contacts Us -->
    <a href="#contact" class="text-white ml-7">Contact Us</a>

    <!-- FAQs -->
    <a href="#FAQ" class="text-white ml-7">FAQs</a>
  </nav>
</div>

<section id="home" class="relative flex-grow h-screen">
  <!-- Image -->
  <enhanced:img class="w-full h-full object-cover" src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="An alt text" />

  <!-- Text overlay -->
  <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center text-white">
    <h1 class="text-4xl font-bold mb-2" style="text-stroke: 2px black; text-shadow: 2px 2px 4px rgba(0, 0, 0, 1);">MV</h1>
    <h2 class="text-2xl font-semibold mb-2" style="text-stroke: 1px black; text-shadow: 2px 2px 3px rgba(0, 0, 0, 1);">MAURITIUS VIGOUR</h2>
    <p class="text-lg" style="text-stroke: 1px black; text-shadow: 2px 2px 2px rgba(0, 0, 0, 1);">We offer the Best and Fresh Products to You.</p>
  </div>
</section>

<section id="products" class="py-10 flex-grow:1 min-h-screen">
  <h2 class="text-3xl font-bold mb-6 text-center">Product Categories</h2>

  <div class="grid grid-cols-1 sm:grid-cols-3 md:grid-cols-3 gap-6">
    <!-- Category 1 -->
    <div class="flex flex-col items-center">
      <div
        class="dropdown-container"
        class:active={ImgDropdowns.dropdown1}
        on:click={() => toggleDrop('dropdown1')}
      >
        <button class="dropdown-button">
          <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 1" />
        </button>
        <p class={textClass}>Category 1</p>

        <div
          class="dropdown-content"
          on:click={(e) => ClickOutside(e, 'dropdown1')}
          on:keydown={(e) => {
            if (e.key === 'Escape') toggleDrop('dropdown1');
          }}
        >
          <a href="#">Option 1</a>
          <a href="#">Option 2</a>
          <a href="#">Option 3</a>
        </div>
      </div>
    </div>

    <!-- Category 2 -->
    <div class="flex flex-col items-center">
      <div
        class="dropdown-container"
        class:active={ImgDropdowns.dropdown2}
        on:click={() => toggleDrop('dropdown2')}
      >
        <button class="dropdown-button">
          <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 2" />
        </button>
        <p class={textClass}>Category 2</p>

        <div
          class="dropdown-content"
          on:click={(e) => ClickOutside(e, 'dropdown2')}
          on:keydown={(e) => {
            if (e.key === 'Escape') toggleDrop('dropdown2');
          }}
        >
          <a href="#">Option 1</a>
          <a href="#">Option 2</a>
          <a href="#">Option 3</a>
        </div>
      </div>
    </div>

    <!-- Category 3 -->
    <div class="flex flex-col items-center">
      <div
        class="dropdown-container"
        class:active={ImgDropdowns.dropdown3}
        on:click={() => toggleDrop('dropdown3')}
      >
        <button class="dropdown-button">
          <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 3" />
        </button>
        <p class={textClass}>Category 3</p>

        <div
          class="dropdown-content"
          on:click={(e) => ClickOutside(e, 'dropdown3')}
          on:keydown={(e) => {
            if (e.key === 'Escape') toggleDrop('dropdown3');
          }}
        >
          <a href="#">Option 1</a>
          <a href="#">Option 2</a>
          <a href="#">Option 3</a>
        </div>
      </div>
    </div>

    <!-- Category 4 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown4}
    on:click={() => toggleDrop('dropdown4')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 4" />
    </button>
    <p class={textClass}>Category 4</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown4')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown4');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

<!-- Category 5 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown5}
    on:click={() => toggleDrop('dropdown5')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 5" />
    </button>
    <p class={textClass}>Category 5</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown5')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown5');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

<!-- Category 6 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown6}
    on:click={() => toggleDrop('dropdown6')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 6" />
    </button>
    <p class={textClass}>Category 6</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown6')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown6');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

<!-- Category 7 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown7}
    on:click={() => toggleDrop('dropdown7')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 7" />
    </button>
    <p class={textClass}>Category 7</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown7')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown7');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

<!-- Category 8 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown8}
    on:click={() => toggleDrop('dropdown8')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 8" />
    </button>
    <p class={textClass}>Category 8</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown8')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown8');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

<!-- Category 9 -->
<div class="flex flex-col items-center">
  <div
    class="dropdown-container"
    class:active={ImgDropdowns.dropdown9}
    on:click={() => toggleDrop('dropdown9')}
  >
    <button class="dropdown-button">
      <enhanced:img class={imageClass} src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="Category 9" />
    </button>
    <p class={textClass}>Category 9</p>

    <div
      class="dropdown-content"
      on:click={(e) => ClickOutside(e, 'dropdown9')}
      on:keydown={(e) => {
        if (e.key === 'Escape') toggleDrop('dropdown9');
      }}
    >
      <a href="#">Option 1</a>
      <a href="#">Option 2</a>
      <a href="#">Option 3</a>
    </div>
  </div>
</div>

  </div>
</section>

<section id="best" class="pt-4 pb-10 flex justify-center bg-white-1">
  <div class="slideshow-container lg:w-full sm:w-full overflow-hidden">
    <h2 class="text-3xl font-bold mb-6 text-center">Best Sellers</h2>
    <div class="mySlides slide-in">
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
      
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
    </div>

    <div class="mySlides slide-in">
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
      
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
    </div>

    <div class="mySlides slide-in">
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
      
      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; margin-right: 5%; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div style="width:21%; float: left; object-fit: cover; aspect-ratio: 1/1;">
        <img src="bg.jpg" style="aspect-ratio: 1/1;object-fit: cover;" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
    </div>
  </div>
  <br>

  <div style="text-align:center">
    <span class="dot"></span> 
    <span class="dot"></span> 
    <span class="dot"></span> 
  </div>
</section>

<section id="about" class="py-10 bg-white-2 text-white text-center">
  <div class="container mx-auto">
    <h2 class="text-3xl font-bold mb-6">ABOUT US</h2>
    
    <p class="mb-4">MV Ltd - Mauritius Vigour is a business vendor established in Mauritius. This business offers a broad range / catalogue of products including:</p>

    <ul class="flex flex-wrap justify-center gap-x-4 list-none mb-4">
      <li class="mx-2">Vegetables</li>
      <li class="mx-2">Fruits</li>
      <li class="mx-2">Fresh Cold Press Juice</li>
      <li class="mx-2">Pizza</li>
      <li class="mx-2">Pasta</li>
      <li class="mx-2">Sauces / Salsa</li>
      <li class="mx-2">SeaFood</li>
      <li class="mx-2">Red Meat</li>
      <li class="mx-2">White Meat</li>
    </ul>

    <p class="mb-6">¡Free Delivery Anywhere in the Island!</p>

    <p class="mb-6">Exquisite Products, Exceptional Packaging.</p>

    <p class="mb-6">Cultivated in Hydroponic Greenhouses, Our Fresh Produce is Pure, Pesticide-Free Perfection.</p>
  </div>
</section>

<section id="contact" class="py-10 bg-white-1 text-white text-center">
  <div class="container mx-auto">
    <h2 class="text-3xl font-bold mb-6">CONTACT US</h2>
    
    <p class="mb-6">Feel free to reach out to us:</p>

    <p class="mb-3">Phone: <a href="tel:+23054588841" class="underline">+230 5458 8841</a></p>
    <p class="mb-6">Email: <a href="mailto:marc.valero2605@gmail.com" class="underline">marc.valero2605@gmail.com</a></p>
  </div>
</section>

<section id="FAQ" class="py-10 bg-white-2 text-white text-center">
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div class="faq-container">
    <h2 class="text-3xl font-bold mb-6">FAQs</h2>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="question" on:click={() => (faqDropdowns.q1 = !faqDropdowns.q1)}  class:active={faqDropdowns.q1}>
      What products do you offer?
    </div>
    <div class="answer" class:active={faqDropdowns.q1}>
      We offer a broad range of products including vegetables, fruits, fresh cold press juice, pizza, pasta, sauces/salsa, seafood, red meat, and white meat.
    </div>

    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class="question" on:click={() => faqDropdowns.q2 = !faqDropdowns.q2} class:active={faqDropdowns.q2}>
      Is there free delivery?
    </div>
    <div class="answer" class:active={faqDropdowns.q2}>
      Yes, we offer free delivery anywhere in the island!
    </div>

    <!-- Add more questions and answers as needed -->
  </div>
</section>

<section id="contact" class="py-10 bg-gray-200">
  <h2 class="text-3xl font-bold mb-6 text-center">Contact Us</h2>

  <form id="contactForm" action="your-server-script.php" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required class="mb-4 p-2 w-full">

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required class="mb-4 p-2 w-full">

    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="4" required class="mb-4 p-2 w-full"></textarea>

    <button type="submit" class="bg-blue-500 text-white p-2 rounded">Submit</button>
  </form>
</section>








