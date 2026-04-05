const DEMO_USER = { email: 'demo@shantanu.dev', password: 'demo123' };

const form = document.getElementById('loginForm');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');
const emailError = document.getElementById('emailError');
const passwordError = document.getElementById('passwordError');
const globalError = document.getElementById('globalError');
const submitBtn = document.getElementById('submitBtn');
const successOverlay = document.getElementById('successOverlay');
const eyeBtn = document.getElementById('eyeBtn');
const eyeIcon = document.getElementById('eyeIcon');

function validateEmail(val) {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(val.trim());
}

function setFieldState(input, errorEl, valid, msg) {
  input.classList.toggle('error-input', !valid);
  input.classList.toggle('success-input', valid && input.value.length > 0);
  if (msg) errorEl.textContent = msg;
  errorEl.classList.toggle('show', !valid);
}

// Validate on blur
emailInput.addEventListener('blur', () => {
  if (emailInput.value) {
    setFieldState(emailInput, emailError, validateEmail(emailInput.value));
  }
});

passwordInput.addEventListener('blur', () => {
  if (passwordInput.value) {
    setFieldState(passwordInput, passwordError, passwordInput.value.length >= 6);
  }
});

// Clear errors on input
emailInput.addEventListener('input', () => {
  if (emailInput.classList.contains('error-input')) {
    setFieldState(emailInput, emailError, validateEmail(emailInput.value));
  }
  globalError.classList.remove('show');
});

passwordInput.addEventListener('input', () => {
  if (passwordInput.classList.contains('error-input')) {
    setFieldState(passwordInput, passwordError, passwordInput.value.length >= 6);
  }
  globalError.classList.remove('show');
});

// Show / hide password
eyeBtn.addEventListener('click', () => {
  const isPassword = passwordInput.type === 'password';
  passwordInput.type = isPassword ? 'text' : 'password';
  eyeIcon.innerHTML = isPassword
    ? `<path d="M17.94 17.94A10.07 10.07 0 0112 20c-7 0-11-8-11-8a18.45 18.45 0 015.06-5.94"/>
       <path d="M9.9 4.24A9.12 9.12 0 0112 4c7 0 11 8 11 8a18.5 18.5 0 01-2.16 3.19"/>
       <line x1="1" y1="1" x2="23" y2="23"/>`
    : `<path d="M1 12s4-8 11-8 11 8 11 8-4 8-11 8-11-8-11-8z"/>
       <circle cx="12" cy="12" r="3"/>`;
});

// Form submit
form.addEventListener('submit', async (e) => {
  e.preventDefault();

  const emailVal = emailInput.value.trim();
  const passVal = passwordInput.value;
  let valid = true;

  if (!validateEmail(emailVal)) {
    setFieldState(emailInput, emailError, false, 'Please enter a valid email address.');
    valid = false;
  } else {
    setFieldState(emailInput, emailError, true);
  }

  if (passVal.length < 6) {
    setFieldState(passwordInput, passwordError, false, 'Password must be at least 6 characters.');
    valid = false;
  } else {
    setFieldState(passwordInput, passwordError, true);
  }

  if (!valid) return;

  // Show loading state
  submitBtn.classList.add('loading');
  submitBtn.disabled = true;
  globalError.classList.remove('show');

  // Simulate API call
  await new Promise(r => setTimeout(r, 1400));

  if (emailVal === DEMO_USER.email && passVal === DEMO_USER.password) {
    submitBtn.classList.remove('loading');
    successOverlay.classList.add('show');
    setTimeout(() => {
      alert('Login successful! (Demo mode — no real redirect)');
      successOverlay.classList.remove('show');
      submitBtn.disabled = false;
    }, 2000);
  } else {
    submitBtn.classList.remove('loading');
    submitBtn.disabled = false;
    globalError.classList.add('show');
    emailInput.classList.add('error-input');
    passwordInput.classList.add('error-input');
  }
});

// Social login placeholder
function socialLogin(provider) {
  alert(`${provider} OAuth would be triggered here.\n(Requires backend integration)`);
}
