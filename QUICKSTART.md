# 🚀 GraphGarnish: Quick Deploy Card

**Your custom domains:** `graph-gist.com` and `graphgist.studio`  
**Your GitHub username:** `dagny099`

---

## ⚡ 10-Minute Deploy (GitHub Pages - Recommended)

### 1️⃣ Create Repo (2 min)
```
1. Go to: https://github.com/new
2. Name: graphgarnish
3. Public ✅
4. Add README ✅
5. License: MIT
6. Create repository
```

### 2️⃣ Upload Files (3 min)
```
1. Click "Add file" → "Upload files"
2. Drag ALL files from deployment/ folder
3. Commit: "Initial commit: GraphGarnish v1.0"
```

### 3️⃣ Enable Pages (2 min)
```
1. Settings → Pages
2. Source: main branch, / (root)
3. Save
4. Wait ~1 minute
5. Test: https://dagny099.github.io/graphgarnish
```

### 4️⃣ Add Custom Domain (3 min)
```
1. In Pages settings, enter: graph-gist.com
2. Save
3. Go to your domain registrar
4. Add these DNS records:

   Type: A      Host: @      Value: 185.199.108.153
   Type: A      Host: @      Value: 185.199.109.153
   Type: A      Host: @      Value: 185.199.110.153
   Type: A      Host: @      Value: 185.199.111.153
   Type: CNAME  Host: www    Value: dagny099.github.io

5. Wait 15-60 min for DNS propagation
6. Check ✅ "Enforce HTTPS" in GitHub
```

### 5️⃣ Second Domain Setup
```
In registrar for graphgist.studio:
- Use "Domain Forwarding" → https://graph-gist.com
- OR add DNS records (but GitHub supports only 1 domain per repo)
```

---

## 🎯 Test Checklist

Once DNS propagates (~1 hour):

- [ ] https://graph-gist.com loads
- [ ] https://www.graph-gist.com loads  
- [ ] https://graphgist.studio redirects
- [ ] Landing page works
- [ ] "Explore Network" button works
- [ ] Filters work
- [ ] File upload works
- [ ] No console errors (F12)

---

## 📝 Post on LinkedIn

**After deployment succeeds:**

1. Use **Option 2** from `GraphGarnish_LinkedIn_Post.md` (Story-Driven)
2. Replace `[Demo coming soon]` with: `https://graph-gist.com`
3. Add screenshot or screen recording
4. Post!

**Pro tip:** Include a call-out in your post like:
> "Try it yourself at graph-gist.com or drop a comment if you want help visualizing your own podcast network."

---

## 🆘 Troubleshooting

**DNS not working?**
- Wait longer (up to 48 hours, usually 1 hour)
- Check with: `nslookup graph-gist.com`
- Clear browser cache

**Site not updating?**
- Hard refresh: Ctrl+F5 (Windows) or Cmd+Shift+R (Mac)
- Wait 1-2 minutes after push
- Check GitHub Actions for errors

**Want more control?**
- See `DEPLOYMENT.md` for EC2 deployment instructions

---

## 📞 Quick Links

- **Repo:** https://github.com/dagny099/graphgarnish
- **GitHub Pages Docs:** https://docs.github.com/en/pages
- **Full Deployment Guide:** See `DEPLOYMENT.md` in this folder
- **README:** See `README.md` for project documentation

---

## 🎉 You're Ready!

Follow the 5 steps above, wait for DNS, then share your live site on LinkedIn!

**Total time:** 10 minutes active work + 1 hour DNS wait

Good luck! 🍸
