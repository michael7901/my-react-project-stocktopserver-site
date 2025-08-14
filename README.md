# StockTopServer

A modern **React** application built with **Vite**, **TypeScript**, and **Tailwind CSS**.  
This project provides a responsive UI and can be deployed easily on **cPanel** or any web server.

---

## 🚀 Features
- ⚡️ Fast build with [Vite](https://vitejs.dev/)
- 🎨 Beautiful UI with [Tailwind CSS](https://tailwindcss.com/)
- 📱 Fully responsive design
- 🔷 Built with TypeScript for type safety
- 🌐 Ready for deployment on cPanel

---

## 🛠 Installation & Setup

### Prerequisites
- Node.js (version 16 or higher recommended)
- npm or yarn package manager
- A cPanel hosting account

### Local Development Setup

1. **Clone the repository:**
```bash
git clone https://github.com/USERNAME/StockTopServer.git
cd StockTopServer
```

2. **Install dependencies:**
```bash
npm install
```

3. **Start the development server:**
```bash
npm run dev
```

The application will be available at `http://localhost:5173`

4. **Build for production:**
```bash
npm run build
```

This creates an optimized production build in the `dist` folder.

---

## 📦 Deploying to cPanel

This guide will walk you through deploying your React + Vite application to cPanel.

### Step 1: Build Your Project

Before deploying, create a production build:

```bash
npm run build
```

This generates optimized static files in the `dist` directory that are ready for deployment.

### Step 2: Prepare Files for Upload

1. **Navigate to the dist folder** after building:
   - Your built files will be in the `dist` folder
   - This folder contains `index.html` and all necessary assets (JS, CSS, images, etc.)

2. **Create a .htaccess file** (Important for React Router and SPA routing):
   
   **Option A:** Copy the `.htaccess.template` file from the project root to your `dist` folder and rename it to `.htaccess`
   
   **Option B:** Create a file named `.htaccess` in your `dist` folder with the following content:

```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```

This ensures that all routes are handled by your React app (necessary for client-side routing).

### Step 3: Upload to cPanel

#### Method 1: Using cPanel File Manager

1. **Log into your cPanel account**

2. **Open File Manager**
   - Navigate to `public_html` (for main domain) or `public_html/subdomain` (for subdomains)

3. **Upload your files:**
   - Option A: Upload the entire contents of the `dist` folder
     - Select all files inside `dist` (including `.htaccess`)
     - Upload them directly to `public_html`
   - Option B: Create a folder (e.g., `myapp`) and upload files there
     - This would make your app available at `yourdomain.com/myapp`

4. **Verify file structure:**
   - Ensure `index.html` is in the root of your deployment directory
   - Verify `.htaccess` file is present
   - Check that all asset folders (assets, images, etc.) are uploaded

#### Method 2: Using FTP/SFTP Client

1. **Connect to your server** using an FTP client (FileZilla, WinSCP, etc.)
   - Host: Your domain or cPanel FTP host
   - Username: Your cPanel username
   - Password: Your cPanel password
   - Port: 21 (FTP) or 22 (SFTP)

2. **Navigate to `public_html`** directory

3. **Upload all files** from your local `dist` folder to `public_html`

4. **Set correct permissions:**
   - Files: `644`
   - Folders: `755`

### Step 4: Verify Deployment

1. **Visit your website** in a browser
   - Main domain: `https://yourdomain.com`
   - Subdomain: `https://subdomain.yourdomain.com`
   - Subfolder: `https://yourdomain.com/myapp`

2. **Test the application:**
   - Check if the page loads correctly
   - Verify all assets (CSS, images) are loading
   - Test navigation and routing if you have client-side routes

### Step 5: Troubleshooting Common Issues

#### Issue: 404 Error on Page Refresh
**Solution:** Ensure `.htaccess` file is uploaded and contains the rewrite rules above.

#### Issue: Assets Not Loading (404 on CSS/JS files)
**Possible causes:**
- Incorrect base path configuration
- Files not uploaded correctly
- Case sensitivity issues (Linux servers are case-sensitive)

**Solution:**
- If deploying to a subdirectory, update `vite.config.ts`:
```typescript
export default defineConfig({
  plugins: [react()],
  base: '/your-subdirectory/', // Add this line
  optimizeDeps: {
    exclude: ['lucide-react'],
  },
});
```
Then rebuild the project.

#### Issue: Blank Page
**Check:**
- Browser console for JavaScript errors
- Network tab to see if files are loading
- Ensure `index.html` exists in the root directory
- Verify file permissions (should be 644 for files, 755 for folders)

#### Issue: Slow Loading
**Optimizations:**
- Ensure you're using the production build (not development files)
- Enable GZIP compression in cPanel (if available)
- Check cPanel's caching settings

---

## 🔧 Configuration Options

### Deploying to a Subdirectory

If you need to deploy to a subdirectory (e.g., `yourdomain.com/myapp`):

1. **Update `vite.config.ts`:**
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  base: '/myapp/', // Change this to your subdirectory
  optimizeDeps: {
    exclude: ['lucide-react'],
  },
});
```

2. **Update `.htaccess`** in the dist folder:
```apache
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /myapp/
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /myapp/index.html [L]
</IfModule>
```

3. **Rebuild:**
```bash
npm run build
```

### Environment Variables

If you need environment variables for production:

1. **Create `.env.production` file:**
```
VITE_API_URL=https://api.yourdomain.com
```

2. **Access in code:**
```typescript
const apiUrl = import.meta.env.VITE_API_URL;
```

3. **Rebuild** after adding environment variables.

---

## 📝 Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build locally
- `npm run lint` - Run ESLint

---

## 🌐 Additional Resources

- [Vite Documentation](https://vitejs.dev/)
- [React Documentation](https://react.dev/)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [cPanel Documentation](https://docs.cpanel.net/)

---

## 📄 License

[Add your license information here]

---

## 🤝 Contributing

[Add contribution guidelines if applicable]
