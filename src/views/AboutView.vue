<template>
  <div class="about">
    <div class="content">
      <h1>Ini isinya Cuman Nyobain </h1>
      <p>Mantap first Time Vue</p>
    </div>
  </div>
</template>

<style scoped>
/* Styling for the main about container */
.about {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #87cefa, #b0e0e6); /* Soft blue gradient */
  padding: 0 16px;
  animation: fadeIn 1.2s ease-in-out; /* Fade-in effect */
}

.content {
  text-align: center;
  background-color: rgba(255, 255, 255, 0.8); /* Transparent background for better readability */
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1); /* Soft shadow for depth */
}

h1 {
  font-size: 2.5rem;
  color: #333;
  margin-bottom: 16px;
  font-family: 'Poppins', sans-serif; /* Modern font */
}

p {
  font-size: 1.25rem;
  color: #555;
  line-height: 1.6;
  margin-bottom: 0;
}

/* Responsive adjustments for larger screens */
@media (min-width: 1024px) {
  .about {
    padding: 0;
  }

  h1 {
    font-size: 3rem;
  }

  p {
    font-size: 1.5rem;
  }
}

/* Fade-in animation */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>
