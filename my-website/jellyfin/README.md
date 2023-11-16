# Branding
```
<p id="quote1">"May I enjoy my life and practice my art, respected by all men and in all times" - R.I. Pharma Motto</p>
<p id="quote2">"Sharing is good, and with digital technology, sharing is easy." - Richard Stallman</p>
<p id="quote3">“You have power over your mind — not outside events. Realize this, and you will find strength.” - Marcus Aurelius</p>
<p id="quote4">DrAnglerfish</p>
```
# Custom CSS code:
```
.skinHeader.focuscontainer-x.skinHeader-withBackground.skinHeader-blurred {
  background: none;
  background-color: rgba(0, 0, 0, 0);
}
.skinHeader.focuscontainer-x.skinHeader-withBackground.skinHeader-blurred.noHomeButtonHeader {
  background: none;
  background-color: rgba(0, 0, 0, 0);
}

.pageTitleWithDefaultLogo {
    background-image: url('https://static.wikia.nocookie.net/mrfz/images/5/55/Strategic_Battle_Record.png/revision/latest?cb=20190813091500');
}

#loginPage {
background-image: url('https://webusstatic.yo-star.com/ark_us_web/pc/img/bg.6cd7a627.png');
  background-size: cover;
  background-position: center;
}

@media (max-width: 768px) {
  #loginPage {
    background-image: url('https://webusstatic.yo-star.com/ark_us_web/pc/img/bg.6cd7a627.png');
    background-size: cover;
    background-position: center;
  }
}

/* Narrow the login form */
#loginPage .readOnlyContent,
#loginPage form {
  max-width: 26em;
}

/* Hide "please login" text, margin is to prevent login form moving too far up */
#loginPage h1 {
  display: none;
}
#loginPage .padded-left.padded-right.padded-bottom-page {
  margin-top: 50px;
}

/* Hide "manual" and "forgot" buttons */
#loginPage .raised.cancel.block.btnManual.emby-button {
  display: none;
}
#loginPage .raised.cancel.block.btnForgotPassword.emby-button {
  display: none;
}

.disclaimerContainer {
  position: relative;
  width: 100%;
  height: 100px;
  overflow: hidden;
}

.disclaimer p {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  margin: 0;
  opacity: 0;
  transform: translateY(100%);
  animation: fadeAndFlow 40s infinite;
}

#quote1 {
  animation-delay: 0s;
}

#quote2 {
  animation-delay: 10s; 
}

#quote3 {
  animation-delay: 20s;
}

#quote4 {
  animation-delay: 30s;
}

@keyframes fadeAndFlow {
  0%, 4% {
    opacity: 0;
    transform: translateY(100%);
  }
  5%, 25% {
    opacity: 1;
    transform: translateY(0);
  }
  30%, 100% {
    opacity: 0;
    transform: translateY(0);
  }
}
```