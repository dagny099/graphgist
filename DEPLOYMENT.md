# 🚀 GraphGarnish Deployment Guide

Complete instructions for deploying GraphGarnish to **GitHub Pages** and **EC2**, with custom domain configuration for `graph-gist.com` and `graphgist.studio`.

---

## 📦 What's in Your Deployment Package

```
deployment/
├── index.html              # Landing page
├── explore.html            # Interactive network visualization
├── sample_network.json     # Demo data (203 episodes)
├── README.md              # Project documentation
├── CNAME                  # Custom domain for GitHub Pages
└── DEPLOYMENT.md          # This file
```

---

## Option 1: GitHub Pages (Recommended for Quick Start)

**Pros:**
- ✅ Free hosting
- ✅ Automatic HTTPS
- ✅ Zero maintenance
- ✅ Git-based deployment
- ✅ Custom domain support
- ✅ CDN included

**Time to deploy:** ~15 minutes

---

### Step 1: Create GitHub Repository

1. **Go to GitHub:** https://github.com/new

2. **Create repository:**
   - Repository name: `graphgarnish`
   - Description: `🍸 Interactive network visualization for podcast metadata`
   - Public (required for free GitHub Pages)
   - ✅ Add README (we'll replace it)
   - ✅ Add .gitignore (Node)
   - License: MIT

3. **Click "Create repository"**

---

### Step 2: Upload Your Files

**Option A: Via GitHub Web Interface (Easiest)**

1. In your new repo, click **"Add file"** → **"Upload files"**

2. Drag and drop ALL files from your `deployment/` folder:
   - `index.html`
   - `explore.html`
   - `sample_network.json`
   - `README.md`
   - `CNAME`

3. Commit message: `Initial commit: GraphGarnish v1.0`

4. Click **"Commit changes"**

**Option B: Via Git Command Line**

```bash
# Navigate to your deployment folder
cd /path/to/deployment

# Initialize git
git init

# Add remote (replace with your actual repo URL)
git remote add origin https://github.com/dagny099/graphgarnish.git

# Add all files
git add .

# Commit
git commit -m "Initial commit: GraphGarnish v1.0"

# Push to GitHub
git branch -M main
git push -u origin main
```

---

### Step 3: Enable GitHub Pages

1. **In your repo, go to:** Settings → Pages (left sidebar)

2. **Source:** Deploy from a branch

3. **Branch:** Select `main` branch, `/ (root)` folder

4. **Click "Save"**

5. **Wait 1-2 minutes** for deployment

6. **Test:** Visit `https://dagny099.github.io/graphgarnish`

---

### Step 4: Configure Custom Domain (graph-gist.com)

#### Part A: GitHub Settings

1. **In GitHub Pages settings**, scroll to **"Custom domain"**

2. **Enter:** `graph-gist.com`

3. **Click "Save"**

4. **Wait for DNS check** (GitHub will verify your domain)

5. **Once verified, check:** ✅ Enforce HTTPS

#### Part B: Domain Registrar (Namecheap/GoDaddy/etc.)

**For `graph-gist.com` to point to GitHub Pages:**

1. **Log in to your domain registrar**

2. **Go to DNS Management** for `graph-gist.com`

3. **Delete existing A records** (if any)

4. **Add these 4 A records:**
   ```
   Type: A    Host: @    Value: 185.199.108.153    TTL: 1 hour
   Type: A    Host: @    Value: 185.199.109.153    TTL: 1 hour
   Type: A    Host: @    Value: 185.199.110.153    TTL: 1 hour
   Type: A    Host: @    Value: 185.199.111.153    TTL: 1 hour
   ```

5. **Add CNAME record** (for www subdomain):
   ```
   Type: CNAME    Host: www    Value: dagny099.github.io    TTL: 1 hour
   ```

6. **Save changes**

7. **Wait 15-60 minutes** for DNS propagation

8. **Test:** 
   - `http://graph-gist.com` → should redirect to your site
   - `https://graph-gist.com` → should work after GitHub enables SSL

---

### Step 5: Configure Second Domain (graphgist.studio)

**Option A: Point to Same GitHub Pages Site**

In your domain registrar for `graphgist.studio`:

```
Type: CNAME    Host: @    Value: dagny099.github.io    TTL: 1 hour
Type: CNAME    Host: www    Value: dagny099.github.io    TTL: 1 hour
```

**Issue:** GitHub Pages only supports ONE custom domain per repo.

**Solution:** Pick your primary domain (`graph-gist.com`), then use a redirect service for the secondary domain.

**Option B: Domain Forwarding (Recommended)**

In your registrar for `graphgist.studio`:

1. **Enable "Domain Forwarding"** or **"URL Redirect"**
2. **Forward to:** `https://graph-gist.com`
3. **Type:** 301 Permanent Redirect
4. **Include path:** Yes

Now both domains work:
- `graph-gist.com` → Primary site (GitHub Pages)
- `graphgist.studio` → Redirects to `graph-gist.com`

---

### Step 6: Verify Deployment

**Test these URLs:**

1. ✅ `https://dagny099.github.io/graphgarnish` (GitHub subdomain)
2. ✅ `https://graph-gist.com` (custom domain)
3. ✅ `https://www.graph-gist.com` (www subdomain)
4. ✅ `https://graphgist.studio` (redirects to graph-gist.com)

**Check functionality:**
- Landing page loads
- "Explore the Network" button works
- Network visualization renders
- Filters work
- File upload works

---

### Step 7: Update Links in Your Files

After deployment, update any placeholder URLs:

1. **In `README.md`**, replace:
   ```markdown
   🔗 **Live Demo:** [graph-gist.com](https://graph-gist.com)
   ```

2. **In your LinkedIn post**, use:
   ```
   🔗 Explore it here: https://graph-gist.com
   ```

3. **Commit changes:**
   ```bash
   git add README.md
   git commit -m "Update live demo URL"
   git push origin main
   ```

---

## GitHub Pages: Troubleshooting

### DNS Not Resolving
- **Wait:** DNS can take up to 48 hours (usually 1 hour)
- **Test:** Use `nslookup graph-gist.com` to check DNS
- **Flush cache:** Clear your browser cache and DNS cache

### SSL Certificate Error
- **Wait:** GitHub takes 10-60 minutes to provision SSL
- **Check:** "Enforce HTTPS" should be checked in GitHub Pages settings
- **Note:** Can't enable HTTPS until DNS is fully propagated

### 404 Errors
- **Check:** Files are in root of `main` branch, not in a subfolder
- **Check:** GitHub Pages is enabled and deployed
- **Check:** `CNAME` file contains correct domain

### Site Not Updating
- **Hard refresh:** Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)
- **Check:** Latest commit is in `main` branch
- **Wait:** GitHub Pages can take 1-2 minutes to rebuild

---

## Option 2: EC2 Deployment

**Pros:**
- ✅ Full control
- ✅ Can run backend services
- ✅ Multiple domains on one instance
- ✅ Custom server configuration

**Cons:**
- ❌ Requires server management
- ❌ Not free (~$3-10/month)
- ❌ Need to handle SSL certificates

**Time to deploy:** ~30 minutes

---

### Prerequisites

- EC2 instance running (Ubuntu 22.04 recommended)
- SSH access to your instance
- Nginx or Apache installed
- Domains registered (`graph-gist.com` and `graphgist.studio`)

---

### Step 1: Prepare Your EC2 Instance

**SSH into your instance:**
```bash
ssh -i your-key.pem ubuntu@your-ec2-ip
```

**Update system:**
```bash
sudo apt update
sudo apt upgrade -y
```

**Install Nginx:**
```bash
sudo apt install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

**Verify:** Visit `http://your-ec2-ip` → should see Nginx welcome page

---

### Step 2: Upload Your Files to EC2

**Option A: Using SCP (Secure Copy)**

From your local machine:
```bash
# Create deployment directory on EC2
ssh -i your-key.pem ubuntu@your-ec2-ip "sudo mkdir -p /var/www/graphgarnish"

# Upload files
scp -i your-key.pem -r deployment/* ubuntu@your-ec2-ip:/tmp/

# Move files to web directory
ssh -i your-key.pem ubuntu@your-ec2-ip "sudo mv /tmp/*.html /tmp/*.json /tmp/*.md /var/www/graphgarnish/"

# Set permissions
ssh -i your-key.pem ubuntu@your-ec2-ip "sudo chown -R www-data:www-data /var/www/graphgarnish"
```

**Option B: Using Git**

On EC2:
```bash
cd /var/www
sudo git clone https://github.com/dagny099/graphgarnish.git
sudo chown -R www-data:www-data /var/www/graphgarnish
```

---

### Step 3: Configure Nginx for graph-gist.com

**Create Nginx config:**
```bash
sudo nano /etc/nginx/sites-available/graphgarnish
```

**Paste this configuration:**
```nginx
server {
    listen 80;
    server_name graph-gist.com www.graph-gist.com;
    
    root /var/www/graphgarnish;
    index index.html;
    
    # Compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml;
    
    # Main location
    location / {
        try_files $uri $uri/ =404;
    }
    
    # Cache static assets
    location ~* \.(json|html|css|js)$ {
        expires 1d;
        add_header Cache-Control "public, immutable";
    }
    
    # Security headers
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;
}
```

**Enable site:**
```bash
sudo ln -s /etc/nginx/sites-available/graphgarnish /etc/nginx/sites-enabled/
sudo nginx -t  # Test configuration
sudo systemctl reload nginx
```

---

### Step 4: Configure DNS for EC2

**In your domain registrar for `graph-gist.com`:**

1. **Add A record:**
   ```
   Type: A
   Host: @
   Value: YOUR-EC2-IP-ADDRESS
   TTL: 1 hour
   ```

2. **Add www CNAME:**
   ```
   Type: CNAME
   Host: www
   Value: graph-gist.com
   TTL: 1 hour
   ```

**Repeat for `graphgist.studio`:**
```
Type: A
Host: @
Value: YOUR-EC2-IP-ADDRESS
TTL: 1 hour
```

**Wait 15-60 minutes for DNS propagation**

**Test:** `http://graph-gist.com` should show your site (no HTTPS yet)

---

### Step 5: Enable HTTPS with Let's Encrypt

**Install Certbot:**
```bash
sudo apt install certbot python3-certbot-nginx -y
```

**Get SSL certificate for both domains:**
```bash
sudo certbot --nginx -d graph-gist.com -d www.graph-gist.com -d graphgist.studio -d www.graphgist.studio
```

**Follow prompts:**
- Enter email address
- Agree to terms
- Choose: Redirect HTTP to HTTPS (recommended)

**Auto-renewal:**
```bash
sudo certbot renew --dry-run  # Test renewal
sudo systemctl status certbot.timer  # Verify auto-renewal is enabled
```

**Test:**
- ✅ `https://graph-gist.com`
- ✅ `https://graphgist.studio`

Both should work with valid SSL!

---

### Step 6: Configure Multiple Domains on EC2

**Edit Nginx config to handle both domains:**
```bash
sudo nano /etc/nginx/sites-available/graphgarnish
```

**Update to:**
```nginx
# Primary site: graph-gist.com
server {
    listen 80;
    listen 443 ssl http2;
    server_name graph-gist.com www.graph-gist.com;
    
    ssl_certificate /etc/letsencrypt/live/graph-gist.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/graph-gist.com/privkey.pem;
    
    root /var/www/graphgarnish;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}

# Secondary site: graphgist.studio (same content)
server {
    listen 80;
    listen 443 ssl http2;
    server_name graphgist.studio www.graphgist.studio;
    
    ssl_certificate /etc/letsencrypt/live/graph-gist.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/graph-gist.com/privkey.pem;
    
    root /var/www/graphgarnish;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```

**Reload:**
```bash
sudo nginx -t
sudo systemctl reload nginx
```

---

### EC2: Troubleshooting

**502 Bad Gateway:**
- Check Nginx is running: `sudo systemctl status nginx`
- Check file permissions: `ls -la /var/www/graphgarnish`
- Check Nginx error log: `sudo tail -f /var/nginx/error.log`

**403 Forbidden:**
- Fix permissions: `sudo chown -R www-data:www-data /var/www/graphgarnish`
- Check index.html exists: `ls /var/www/graphgarnish/index.html`

**DNS Not Resolving:**
- Check A records point to correct EC2 IP
- Verify security group allows port 80 and 443
- Test with `dig graph-gist.com`

**SSL Certificate Issues:**
- Re-run Certbot: `sudo certbot --nginx --force-renewal`
- Check certificate: `sudo certbot certificates`

---

## 🎉 Post-Deployment Checklist

Once deployed, test these:

### Functionality
- [ ] Landing page loads
- [ ] "Explore Network" button works
- [ ] Network visualization renders with demo data
- [ ] Filters work (year, search, node types, thresholds)
- [ ] Click-to-focus selection works
- [ ] File upload works with custom JSON
- [ ] Responsive design works on mobile

### SEO & Performance
- [ ] HTTPS enabled and forced
- [ ] Custom domain(s) working
- [ ] Meta tags present (view page source)
- [ ] Fast loading (< 2 seconds)
- [ ] No console errors (F12 developer tools)

### Social Sharing
- [ ] Share on LinkedIn with live link
- [ ] Share on Twitter
- [ ] Add to your portfolio/website
- [ ] Update GitHub profile README with link

---

## 🔄 Updating Your Site

### GitHub Pages
```bash
# Make changes locally
git add .
git commit -m "Description of changes"
git push origin main

# GitHub Pages auto-deploys in 1-2 minutes
```

### EC2
```bash
# SSH into EC2
ssh -i your-key.pem ubuntu@your-ec2-ip

# Pull latest changes (if using Git)
cd /var/www/graphgarnish
sudo git pull origin main

# Or upload new files via SCP
scp -i your-key.pem updated-file.html ubuntu@your-ec2-ip:/tmp/
sudo mv /tmp/updated-file.html /var/www/graphgarnish/

# No nginx reload needed for static files
```

---

## 📊 Analytics (Optional)

Add Google Analytics to track visitors:

1. **Get tracking code** from Google Analytics

2. **Add to `index.html` and `explore.html`** before `</head>`:
   ```html
   <!-- Google Analytics -->
   <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
   <script>
     window.dataLayer = window.dataLayer || [];
     function gtag(){dataLayer.push(arguments);}
     gtag('js', new Date());
     gtag('config', 'GA_MEASUREMENT_ID');
   </script>
   ```

3. **Redeploy**

---

## 🆘 Need Help?

**GitHub Pages Issues:**
- https://docs.github.com/en/pages/getting-started-with-github-pages/troubleshooting-404-errors-for-github-pages-sites

**EC2/Nginx Issues:**
- Nginx docs: https://nginx.org/en/docs/
- Let's Encrypt: https://letsencrypt.org/docs/

**GraphGarnish Issues:**
- Open issue: https://github.com/dagny099/graphgarnish/issues

---

## 🎯 Next Steps

1. **Deploy using your preferred method**
2. **Test thoroughly**
3. **Post on LinkedIn** with live link
4. **Share with podcast community**
5. **Iterate based on feedback**

---

**You're ready to launch! 🚀**

Choose your deployment path and follow the steps. GitHub Pages is fastest; EC2 gives you more control. Both work great for GraphGarnish.

Questions? Open an issue on GitHub or reach out on LinkedIn.

*Happy visualizing!*
