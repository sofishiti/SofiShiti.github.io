// Smooth scrolling for navigation links
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function(e) {
        e.preventDefault();
        const targetId = this.getAttribute('href');
        if(targetId === '#') return;
        
        const targetElement = document.querySelector(targetId);
        if(targetElement) {
            window.scrollTo({
                top: targetElement.offsetTop - 80,
                behavior: 'smooth'
            });
            
            // Close mobile menu if open
            const mobileMenu = document.querySelector('.mobile-menu');
            if(mobileMenu && mobileMenu.classList.contains('active')) {
                mobileMenu.classList.remove('active');
            }
        }
    });
});

// Form submission
document.querySelector('.contact-form').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // Get form data
    const formData = {
        name: this.querySelector('input[type="text"]').value,
        phone: this.querySelector('input[type="tel"]').value,
        email: this.querySelector('input[type="email"]').value,
        service: this.querySelector('select').value,
        date: this.querySelector('input[type="date"]').value,
        time: this.querySelector('input[type="time"]').value,
        message: this.querySelector('textarea').value
    };
    
    // Simple validation
    if(!formData.name || !formData.phone || !formData.date || !formData.time) {
        alert('Please fill in all required fields');
        return;
    }
    
    // Here you would normally send data to server
    // For demo, just show success message
    
    alert(`Thank you ${formData.name}! Your appointment request has been received.\nWe will contact you at ${formData.phone} to confirm.`);
    
    // Reset form
    this.reset();
});

// Current year in footer
document.addEventListener('DOMContentLoaded', function() {
    const yearSpan = document.querySelector('.current-year');
    if(yearSpan) {
        yearSpan.textContent = new Date().getFullYear();
    }
    
    // Set minimum date to today for appointment booking
    const dateInput = document.querySelector('input[type="date"]');
    if(dateInput) {
        const today = new Date().toISOString().split('T')[0];
        dateInput.min = today;
    }
});

// Add mobile menu functionality
document.addEventListener('DOMContentLoaded', function() {
    // Create mobile menu button
    const nav = document.querySelector('nav');
    const mobileMenuBtn = document.createElement('button');
    mobileMenuBtn.innerHTML = '<i class="fas fa-bars"></i>';
    mobileMenuBtn.className = 'mobile-menu-btn';
    nav.appendChild(mobileMenuBtn);
    
    // Clone navigation links for mobile
    const navLinks = document.querySelector('.nav-links');
    const mobileNav = navLinks.cloneNode(true);
    mobileNav.className = 'mobile-nav';
    
    // Add to body
    document.body.appendChild(mobileNav);
    
    // Toggle mobile menu
    mobileMenuBtn.addEventListener('click', function() {
        mobileNav.classList.toggle('active');
        this.innerHTML = mobileNav.classList.contains('active') ? 
            '<i class="fas fa-times"></i>' : '<i class="fas fa-bars"></i>';
    });
    
    // Close mobile menu when clicking outside
    document.addEventListener('click', function(e) {
        if(!mobileNav.contains(e.target) && !mobileMenuBtn.contains(e.target)) {
            mobileNav.classList.remove('active');
            mobileMenuBtn.innerHTML = '<i class="fas fa-bars"></i>';
        }
    });
});
