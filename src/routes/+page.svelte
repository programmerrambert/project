<!-- src/routes/index.svelte -->
<script>
  import '../routes/global.css';
  import './__layout.svelte';

  let imageClass = "sm:w-28 md:w-32 lg:w-40 xl:w-48 h-full sm:h-28 md:h-32 lg:h-40 xl:h-48 object-cover rounded-t-lg";
  let textClass = "text-center bg-white-2 rounded-b-lg  sm:w-28 md:w-32 lg:w-40 xl:w-48 pt-1 pb-1 text-s"
  let textClass2 = "text-center bg-white-2"

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

</script>

<style>
  * {box-sizing: border-box;}
  .mySlides {display: none;}


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
    animation-duration: 2s;
    opacity: 1; /* Ensure that the initial state is fully opaque */
    transition: opacity 2s ease-in-out; /* Add a smooth transition for opacity */
  }

  @keyframes slideIn {
    from {
      transform: translateX(100%);
      opacity: 0; /* Start with opacity set to 0 */
    }
    to {
      transform: translateX(0);
      opacity: 1; /* End with opacity set to 1 */
    }
  }
  
  .best {
    width:21%; 
    float: left; 
    margin-right: 5%; 
    object-fit: cover; 
    aspect-ratio: 1/1;
  }

  .img{
    aspect-ratio: 1/1;
    object-fit: cover;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
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

  #contact {
      display: flex;
      justify-content: center;
      align-items: center;
    }

    #contactForm {
      text-align: left;
      width: 80%; /* Adjust the width as needed */
      max-width: 700px; /* Set a maximum width for responsiveness */
    }    
  </style>



<div id="yourFixedNavbar" class="bg-white-1 pt-2 sm:pt-3  sm:pb-3 pl-2 pr-2 fixed top-0 w-full z-10 max-w-screen-xl">
  <!-- Tailwind CSS styling for the navbar -->
  <nav class="flex justify-self-start items-center border-b-white border-b-2 pb-4">
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
          stroke-linejoin="round"`
          stroke-width="2"
          d="M12 19l9 2-9-18-9 18 9-2zm0 0v-8"
        />
      </svg>
    </a>

    <a href="#home" class="text-white text-m">Home</a>

    <!-- Products -->
    <a href="#products" class="text-white ml-7 text-m">Products</a>

    <!-- About Us -->
    <a href="#about" class="text-white ml-7 text-m">About Us</a>

    <!-- Contacts Us -->
    <a href="#contact" class="text-white ml-7 text-m">Contact Us</a>

    <!-- FAQs -->
    <a href="#FAQ" class="text-white ml-7 text-m">FAQs</a>

    <!-- Order -->
    <a href="#Order" class="text-white ml-7 text-m">Order</a>
  </nav>
</div>

<body class="bg-white-1
sm:pl-8 md:pl-12 lg:pl-16 xl:pl-20
sm:pr-8 md:pr-12 lg:pr-16 xl:pr-20
mt-11">

  <section id="home">`
  <!-- Image -->
  <enhanced:img class="w-full object-cover relative h-screen items-center flex-grow-1 rounded-lg" src="D:\Desktop\Svelte\Project\static\bg.jpg" alt="An alt text" />

  <!-- Text overlay -->
  <div class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-center text-white">
    <h1 class="text-4xl font-bold mb-2" style="text-stroke: 2px black; text-shadow: 2px 2px 4px rgba(0, 0, 0, 1);">MV</h1>
    <h2 class="text-2xl font-semibold mb-2" style="text-stroke: 1px black; text-shadow: 2px 2px 3px rgba(0, 0, 0, 1);">MAURITIUS VIGOUR</h2>
    <p class="text-lg" style="text-stroke: 1px black; text-shadow: 2px 2px 2px rgba(0, 0, 0, 1);">We offer the Best and Fresh Products to You.</p>
  </div>
</section>


<section id="products" class="py-10 flex-grow-1 border-2 rounded-lg mt-2 mb-2 h-fit">
  <h2 class="text-3xl font-bold mb-6 text-center">Product Categories</h2>

  <div class="grid grid-cols-3 sm:grid-cols-3 md:grid-cols-3 gap-4">
    <!-- Category 1 -->
    <div class="flex flex-col items-center">
        <img src="bg.jpg" class={imageClass} alt="">
        <p class={textClass}>Hello</p>
    </div>

    <!-- Category 2 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 3 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 4 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 5 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 6 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 7 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 8 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

    <!-- Category 9 -->
    <div class="flex flex-col items-center">
      <img src="bg.jpg" class={imageClass} alt="">
      <p class={textClass}>Hello</p>
  </div>

  </div>
</section>


<section id="best" class="border-2 rounded-lg mt-2 mb-2 flex justify-center bg-white-1">
  <div class="slideshow-container lg:w-full sm:w-full overflow-hidden">
    <h2 class="text-3xl font-bold mb-6 text-center">Best Sellers</h2>
    <div class="mySlides slide-in">
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p class={textClass2}>Hello</p>
        <p class={textClass}>$19.99</p>
      </div>
      
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best" style="margin-right: 0;">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
    </div>

    <div class="mySlides slide-in">
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
      
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best" style="margin-right: 0;">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
    </div>

    <div class="mySlides slide-in">
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>
      
      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best">
        <img src="bg.jpg" class="img" alt="">
        <p style="color: white;">Hello</p>
        <p style="color: white;">$19.99</p>
      </div>

      <div class="best" style="margin-right: 0;">
        <img src="bg.jpg" class="img" alt="">
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


<section id="about" class="py-10 bg-white-2 text-white text-center border-2 rounded-lg mt-2 mb-2">
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


<section id="contact" class="py-10 bg-white-1 text-white text-center border-2 rounded-lg mt-2 mb-2">
  <div class="container mx-auto">
    <h2 class="text-3xl font-bold mb-6">CONTACT US</h2>
    
    <p class="mb-6">Feel free to reach out to us:</p>

    <p class="mb-3">Phone: <a href="tel:+23054588841" class="underline">+230 5458 8841</a></p>
    <p class="mb-6">Email: <a href="mailto:marc.valero2605@gmail.com" class="underline">marc.valero2605@gmail.com</a></p>
  </div>
</section>


<section id="FAQ" class="py-10 bg-white-2 text-white text-centerborder-2 rounded-lg mt-2 mb-2">
  
  <!-- svelte-ignore a11y-no-static-element-interactions -->
  <div class="faq-container">
    <h2 class="text-3xl font-bold mb-6 text-center">FAQs</h2>

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

<section  class="py-10 bg-gray-200 border-2 rounded-lg mt-2 mb-2">
  <h2 id="Order" class="text-3xl font-bold mb-6 text-center">Order</h2>
  <div id="contact">
      <form id="contactForm" action="your-server-script.php" method="post" class="w-4/5 content-center">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required class="mb-4 p-2 w-full rounded-md">

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required class="mb-4 p-2 w-full rounded-md">

    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="4" required class="mb-4 p-2 w-full rounded-md"></textarea>

    <button type="submit" class=" bg-slate-800 text-white p-2 rounded">Submit</button>
  </form>
  </div>
  
  
</section>

</body>









