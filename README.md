# 🚀 Sudesh Ainapure - Portfolio Website

[![Live Demo](https://img.shields.io/badge/Live-Demo-brightgreen?style=for-the-badge)](https://sudeshainapure18-ship-it.github.io/portfolio/)
[![GitHub](https://img.shields.io/badge/GitHub-Profile-blue?style=for-the-badge&logo=github)](https://github.com/sudeshainapure18-ship-it)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/sudesh-ainapure-471b55378)

## 👨‍💻 About

Professional portfolio website showcasing my journey as an **AWS Cloud & DevOps Engineer**. Built with modern web technologies featuring stunning animations, responsive design, and interactive elements.

## ✨ Features

- 🎨 **Modern Design** - Clean, professional UI with AWS-themed color scheme
- 🌊 **Smooth Animations** - Scroll-triggered animations and smooth transitions
- 📱 **Fully Responsive** - Optimized for mobile, tablet, and desktop
- 🎭 **3D Effects** - Interactive 3D tilt effects on project cards
- ⚡ **Particle Background** - Dynamic particle.js background
- 🎯 **Smooth Scrolling** - Seamless navigation between sections
- 📊 **Animated Stats** - Counter animations for statistics
- 💼 **Project Showcase** - Detailed project cards with hover effects
- 📝 **Contact Form** - Integrated with Google Sheets
- 🎨 **Floating Icons** - Animated AWS, Linux, Cloud icons
- 🖱️ **Cursor Trail** - Custom cursor trail effect (desktop only)

## 🛠️ Technologies Used

- **HTML5** - Semantic markup
- **CSS3** - Modern styling with animations
- **JavaScript** - Interactive functionality
- **Particles.js** - Particle background effects
- **Font Awesome** - Icon library
- **Google Sheets API** - Contact form integration

## 📂 Project Structure

```
portfolio/
├── index.html          # Main HTML file
├── style.css           # Stylesheet with animations
├── script.js           # JavaScript functionality
└── README.md           # Project documentation
```

## 🎨 Color Scheme

- **Primary**: `#FF6B35` (Orange)
- **Secondary**: `#F7931E` (Golden Orange)
- **Accent**: `#00D9FF` (Cyan)
- **Dark Background**: `#0A0E27`
- **Darker Background**: `#050816`
- **Card Background**: `#1A1F3A`

## 🚀 Quick Start

### View Live

Visit the live website: [https://sudeshainapure18-ship-it.github.io/portfolio/](https://sudeshainapure18-ship-it.github.io/portfolio/)

### Run Locally

1. Clone the repository:
```bash
git clone https://github.com/sudeshainapure18-ship-it/portfolio.git
```

2. Navigate to the project directory:
```bash
cd portfolio
```

3. Open `index.html` in your browser or use a local server:
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx http-server
```

4. Visit `http://localhost:8000` in your browser

## 📧 Contact Form Setup

To enable the contact form to send data to Google Sheets:

1. Create a Google Sheet with columns: `Name`, `Email`, `Subject`, `Message`, `Timestamp`
2. Go to **Extensions > Apps Script**
3. Add the following script:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  
  sheet.appendRow([
    data.name,
    data.email,
    data.subject,
    data.message,
    data.timestamp
  ]);
  
  return ContentService.createTextOutput(JSON.stringify({result: 'success'}))
    .setMimeType(ContentService.MimeType.JSON);
}
```

4. Deploy as **Web App** with access set to "Anyone"
5. Copy the Web App URL
6. Replace `YOUR_GOOGLE_SHEETS_WEB_APP_URL_HERE` in `script.js` with your URL

## 📱 Sections

1. **Home** - Hero section with introduction and profile
2. **About** - Brief overview and statistics
3. **Skills** - Technical skills with animated progress bars
4. **Projects** - Featured projects with descriptions
5. **Experience** - Work experience and education timeline
6. **Contact** - Contact form and social links

## 🎯 Key Highlights

- ✅ AWS Cloud expertise (EC2, ALB, Auto Scaling, VPC, CloudWatch)
- ✅ Linux system administration
- ✅ Cloud architecture design
- ✅ Full-stack web development
- ✅ Database management (SQL, MariaDB)
- ✅ Backend development (PHP)

## 📊 Projects Featured

### 1. Student Registration System
Dynamic web application for student data management using AWS EC2, PHP, and MariaDB.

### 2. Auto Scaling Group with ALB
Highly available AWS architecture with Auto Scaling Groups and Application Load Balancer.

## 🤝 Connect With Me

- 📧 Email: [sudeshainapure18@gmail.com](mailto:sudeshainapure18@gmail.com)
- 💼 LinkedIn: [Sudesh Ainapure](https://www.linkedin.com/in/sudesh-ainapure-471b55378)
- 🐙 GitHub: [@sudeshainapure18-ship-it](https://github.com/sudeshainapure18-ship-it)

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🙏 Acknowledgments

- Particles.js for the amazing particle effects
- Font Awesome for the icon library
- Google Fonts for typography
- Inspiration from modern portfolio designs

---

⭐ **Star this repository if you found it helpful!**

Made with ❤️ by Sudesh Ainapure