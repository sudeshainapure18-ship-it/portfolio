# 📥 How to Add Resume Download Button

## Quick Manual Update (5 minutes)

### Step 1: Edit index.html

1. Go to: https://github.com/sudeshainapure18-ship-it/portfolio
2. Click on `index.html`
3. Click the **pencil icon** (✏️) to edit
4. Press `Ctrl+F` (or `Cmd+F`) and search for: `<div class="hero-buttons">`
5. You'll find this code (around line 49-56):

```html
<div class="hero-buttons">
    <a href="#contact" class="btn btn-primary">
        <i class="fas fa-envelope"></i> Get In Touch
    </a>
    <a href="#projects" class="btn btn-secondary">
        <i class="fas fa-code"></i> View Projects
    </a>
</div>
```

6. **Replace it with this:**

```html
<div class="hero-buttons">
    <a href="#contact" class="btn btn-primary">
        <i class="fas fa-envelope"></i> Get In Touch
    </a>
    <a href="https://nyc3.digitaloceanspaces.com/bhindi-drive/files/b79dae1a-add2-44de-ad75-f27605c6350c/2026-01-06T14-57-40-838Z-14559e63-sudesh_resume.pdf" 
       class="btn btn-secondary" 
       download="Sudesh_Ainapure_Resume.pdf"
       target="_blank">
        <i class="fas fa-download"></i> Download Resume
    </a>
    <a href="#projects" class="btn btn-outline">
        <i class="fas fa-code"></i> View Projects
    </a>
</div>
```

7. Click **Commit changes**
8. Add commit message: "Add resume download button"
9. Click **Commit changes** again

### Step 2: Add CSS for outline button

1. Go back to repository
2. Click on `style.css`
3. Click the **pencil icon** (✏️) to edit
4. Scroll to the **very bottom** of the file
5. Add this CSS code:

```css
/* Resume Download Button - Outline Style */
.btn-outline {
    background: transparent;
    color: #FF6B35;
    border: 2px solid #FF6B35;
    padding: 12px 30px;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 600;
    display: inline-flex;
    align-items: center;
    gap: 10px;
    transition: all 0.3s ease;
}

.btn-outline:hover {
    background: #FF6B35;
    color: white;
    transform: translateY(-3px);
    box-shadow: 0 10px 30px rgba(255, 107, 53, 0.4);
}

.btn-outline i {
    font-size: 1.1em;
}

/* Make buttons responsive on mobile */
@media (max-width: 768px) {
    .hero-buttons {
        flex-direction: column;
        gap: 15px;
    }
    
    .hero-buttons .btn {
        width: 100%;
        justify-content: center;
    }
}
```

6. Click **Commit changes**
7. Add commit message: "Add styles for resume download button"
8. Click **Commit changes** again

### Step 3: Test Your Website

1. Wait 2-3 minutes for GitHub Pages to update
2. Visit: https://sudeshainapure18-ship-it.github.io/portfolio/
3. You should see 3 buttons:
   - **Get In Touch** (orange)
   - **Download Resume** (orange) ← NEW!
   - **View Projects** (outline)
4. Click "Download Resume" - it should download your PDF!

## ✅ Done!

Your portfolio now has a working resume download button! 🎉

---

## 🎨 What the Buttons Look Like

- **Get In Touch**: Solid orange button
- **Download Resume**: Solid orange button with download icon
- **View Projects**: Outline button (transparent with orange border)

All buttons have hover effects and are fully responsive on mobile!

---

## 🔧 Troubleshooting

**Button not appearing?**
- Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R)
- Wait 3 minutes for GitHub Pages to update

**Resume not downloading?**
- Check that the URL is correct in the code
- Make sure the PDF file is accessible

**Buttons look weird on mobile?**
- Make sure you added the CSS code at the end of style.css
- The responsive CSS will stack buttons vertically on mobile

---

Need help? Let me know!