# Ex05 Image Carousel
## NAME: MADHAN S
## REG NO: 212224040175

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM

## App.js
```
import React from "react";
import Carousel from "./Carousel";

function App() {
  return <Carousel />;
}

export default App;
```

## App.css
```
body {
  margin: 0;
}
```

## Carousel.js
```
import React, { useState, useEffect } from "react";
import "./Carousel.css";

const images = [
  {
    url: "https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?w=1200",
    title: "Explore Nature",
    description: "Discover the beauty of the world around you."
  },
  {
    url: "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?w=1200",
    title: "Ocean Dreams",
    description: "Relax with the peaceful view of the ocean."
  },
  {
    url: "https://images.unsplash.com/photo-1464822759023-fed622ff2c3b?w=1200",
    title: "Mountain Escape",
    description: "Experience the calmness of the mountains."
  },
  {
    url: "https://images.unsplash.com/photo-1493246507139-91e8fad9978e?w=1200",
    title: "Green Paradise",
    description: "Enjoy the freshness of nature."
  }
];

function Carousel() {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextSlide = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const previousSlide = () => {
    setCurrentIndex(
      (currentIndex - 1 + images.length) % images.length
    );
  };

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrentIndex((currentIndex) => (currentIndex + 1) % images.length);
    }, 3000);

    return () => clearInterval(interval);
  }, []);

  return (
    <div className="carousel-page">

      <div className="heading">
        <p>REACT PROJECT</p>
        <h1>Image Carousel</h1>
        <span>Explore moments, one slide at a time.</span>
      </div>

      <div className="carousel">

        <img
          src={images[currentIndex].url}
          alt={images[currentIndex].title}
        />

        <button className="arrow left" onClick={previousSlide}>
          &#10094;
        </button>

        <button className="arrow right" onClick={nextSlide}>
          &#10095;
        </button>

        <div className="caption">
          <h2>{images[currentIndex].title}</h2>
          <p>{images[currentIndex].description}</p>
        </div>

        <div className="counter">
          {currentIndex + 1} / {images.length}
        </div>
      </div>

      <div className="dots">
        {images.map((_, index) => (
          <button
            key={index}
            className={currentIndex === index ? "dot active" : "dot"}
            onClick={() => setCurrentIndex(index)}
          ></button>
        ))}
      </div>

      <div className="auto-play">
        ● Auto playing every 3 seconds
      </div>

    </div>
  );
}

export default Carousel;
```

## Carousel.css
```
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
}

.carousel-page {
  min-height: 100vh;
  background: linear-gradient(135deg, #16002f, #4b126d, #16002f);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px 20px;
  color: white;
}

.heading {
  text-align: center;
  margin-bottom: 25px;
}

.heading p {
  font-size: 13px;
  letter-spacing: 4px;
  margin: 0 0 8px;
  opacity: 0.7;
}

.heading h1 {
  font-size: 42px;
  margin: 0;
}

.heading span {
  display: block;
  margin-top: 8px;
  opacity: 0.7;
}

.carousel {
  width: 850px;
  max-width: 95vw;
  height: 500px;
  position: relative;
  overflow: hidden;
  border-radius: 25px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.carousel img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    transparent 40%,
    rgba(0, 0, 0, 0.8)
  );
}

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 3;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: none;
  background: rgba(255, 255, 255, 0.2);
  color: white;
  font-size: 25px;
  cursor: pointer;
  backdrop-filter: blur(8px);
  transition: 0.3s;
}

.arrow:hover {
  background: white;
  color: #4b126d;
  transform: translateY(-50%) scale(1.1);
}

.left {
  left: 20px;
}

.right {
  right: 20px;
}

.caption {
  position: absolute;
  bottom: 35px;
  left: 40px;
  z-index: 3;
}

.caption h2 {
  margin: 0 0 8px;
  font-size: 30px;
}

.caption p {
  margin: 0;
  opacity: 0.85;
}

.counter {
  position: absolute;
  right: 30px;
  bottom: 35px;
  z-index: 3;
  background: rgba(255, 255, 255, 0.2);
  padding: 8px 15px;
  border-radius: 20px;
}

.dots {
  display: flex;
  gap: 10px;
  margin-top: 20px;
}

.dot {
  width: 10px;
  height: 10px;
  border: none;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.4);
  cursor: pointer;
  transition: 0.3s;
}

.dot.active {
  width: 28px;
  border-radius: 10px;
  background: white;
}

.auto-play {
  margin-top: 15px;
  font-size: 13px;
  opacity: 0.6;
}

@media (max-width: 700px) {
  .carousel {
    height: 400px;
  }

  .heading h1 {
    font-size: 32px;
  }

  .caption {
    left: 25px;
    bottom: 25px;
  }

  .caption h2 {
    font-size: 23px;
  }
}
```


## OUTPUT

<img width="1897" height="1089" alt="image" src="https://github.com/user-attachments/assets/18099c0c-df42-4961-a2a7-4b8c5896314b" />

<img width="1904" height="1086" alt="image" src="https://github.com/user-attachments/assets/cd87cd1b-78e1-4ef4-a3fa-89421179ec46" />

<img width="1893" height="1021" alt="image" src="https://github.com/user-attachments/assets/d8e9b56a-afdf-46d5-b8a0-92c6170dd12b" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
