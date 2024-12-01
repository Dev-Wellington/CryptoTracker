<script setup></script>
<template>
  <div class="user-profile">
    <div class="user-profile__image">
      <img src="../assets/icons/me.png" alt="User Image" />
    </div>
    <div class="user-profile__info">
      <div class="user-profile__name">
        <h3>Wellington</h3>
      </div>
      <div class="user-profile__social-links">
        <ul class="social-links__list">
          <li class="social-links__item">
            <a
              class="social-links__image"
              href="https://github.com/Dev-Wellington/"
              target="_blank"
              ><img src="../assets/icons/github.svg" alt="GitHub"
            /></a>
          </li>
          <li class="social-links__item">
            <a
              class="social-links__image"
              href="https://www.linkedin.com/in/wellington-ds-silva/"
              target="_blank"
              ><img src="../assets/icons/linkedin.svg" alt="LinkedIn"
            /></a>
          </li>
          <li class="social-links__item">
            <a class="social-links__image" href="portfolio.com"
              ><img src="../assets/icons/click.svg" alt="Portfolio"
            /></a>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.user-profile {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 35px;
  width: clamp(250px, 40%, 335px);
  height: clamp(200px, 40vh, 355px);
  border-radius: 35px;
  background-color: var(--bg-profile);
  transition: background-color 0.3s;

}

.user-profile__image {
  width: clamp(65px, 20vw, 130px);
  height: clamp(65px, 20vw, 130px);
}

.user-profile__image img {
  width: 100%;
  height: 100%;
  border-radius: 100%;
  object-fit: cover;
}

.user-profile__info {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.user-profile__name {
  display: flex;
  align-items: center;
  justify-content: center;
  width: clamp(130px, 75%, 200px);
  height: clamp(20px, 25%, 40px);
  border-radius: clamp(25px, 5vw, 50px);
  background-color: var(--bg-profile-name);
}

.user-profile__name h3 {
  font-size: clamp(1.2rem, 3vw, 1.6rem);
  color: var(--text-name);
}

.social-links__list {
  display: flex;
  flex-direction: row;
  list-style: none;
  gap: 18px;
}

.social-links__item {
  height: clamp(45px, 5vw, 60px);
  width: clamp(45px, 5vw, 60px);
}

.social-links__image {
  width: 100%;
  height: 100%;
}

.social-links__image img {
  width: 100%;
  height: 100%;
}
@media (width <= 480px){
  .user-profile {
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 200px;
    gap: 40px;
  }
  .user-profile__image {
    width: 100px;
    height: 100px;
  }
  .user-profile__info {
    flex-direction: column;
    align-items: flex-start;
    gap: 25px; 
  }
}
@media (width > 1280px) {
  .user-profile {
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: clamp(300px, 40%, 500px);
    gap: 40px;
  }
  
  .user-profile__info {
    flex-direction: column;
    align-items: flex-start;
    gap: 25px; 
  }
}
</style>
