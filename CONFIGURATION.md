# ExpenseOwl Configuration Guide

This guide shows you exactly what to configure and where - no guesswork needed!

## 📁 Your Configuration Files

ExpenseOwl now has **two simple files** you can safely edit to customize everything:

### 1. `.env` - Server & Storage Settings
**Location:** Root directory (copy from `.env.example`)

This file controls:
- What port the app runs on
- Where your data is stored
- Database settings (if using PostgreSQL)

### 2. `user-defaults.json` - Your Personal Preferences
**Location:** Root directory

This file controls your initial:
- Expense categories
- Currency
- Billing cycle start date
- Theme preference

---

## 🚀 Quick Start (3 Steps)

### Step 1: Create Your Configuration File
```bash
# Copy the example file to create your config
cp .env.example .env
```

### Step 2: Edit Your Settings (Optional)
The defaults work great for most people! But if you want to customize:

**Edit `.env`** - Change the port or storage location
```bash
PORT=8080              # Change if another app uses port 8080
STORAGE_TYPE=json      # Keep as "json" for simple file storage
STORAGE_URL=data       # Folder where your data is saved
```

**Edit `user-defaults.json`** - Customize your categories and currency
```json
{
  "categories": [
    "Food",
    "Groceries",
    "Your Custom Category Here"
  ],
  "currency": "usd",
  "startDate": 1
}
```

### Step 3: Start the App
```bash
# Using Docker
docker-compose up

# OR run directly with Go
go run cmd/expenseowl/main.go
```

Then open **http://localhost:8080** in your browser!

---

## ⚙️ Configuration Reference

### `.env` File Settings

| Setting | What It Does | Default | Examples |
|---------|--------------|---------|----------|
| `PORT` | Web server port | `8080` | `8080`, `3000`, `9000` |
| `STORAGE_TYPE` | How to store data | `json` | `json` or `postgres` |
| `STORAGE_URL` | Where to store data | `data` | `data`, `/var/lib/expenseowl`, `postgres://...` |
| `DEFAULT_CURRENCY` | Starting currency | `usd` | `usd`, `eur`, `gbp`, `jpy` |
| `DEFAULT_START_DATE` | Billing cycle day | `1` | `1` to `31` |
| `MAX_UPLOAD_SIZE_MB` | CSV upload limit | `10` | `10`, `20`, `50` |

**PostgreSQL Only Settings:**
| Setting | What It Does |
|---------|--------------|
| `STORAGE_USER` | Database username |
| `STORAGE_PASS` | Database password |
| `STORAGE_SSL` | SSL mode: `disable`, `require`, `verify-full` |

### `user-defaults.json` File Settings

```json
{
  "categories": [...]     // Your expense categories
  "currency": "usd",      // Currency code (lowercase)
  "startDate": 1,         // Day of month (1-31) for billing cycle
  "theme": "system"       // "system", "light", or "dark"
}
```

**Supported Currencies:**
`usd`, `eur`, `gbp`, `jpy`, `cny`, `krw`, `inr`, `rub`, `brl`, `zar`, `aed`, `aud`, `cad`, `chf`, `hkd`, `bdt`, `sgd`, `thb`, `try`, `mxn`, `php`, `pln`, `sek`, `nzd`, `dkk`, `idr`, `ils`, `vnd`, `myr`, `mad`

---

## 💡 Common Customizations

### Change the Port
If port 8080 is already in use:

**In `.env`:**
```bash
PORT=3000
```

Then access the app at `http://localhost:3000`

### Use Different Categories
Want different expense categories?

**In `user-defaults.json`:**
```json
{
  "categories": [
    "Salary",
    "Freelance Income",
    "Housing",
    "Transportation",
    "Dining Out",
    "Subscriptions",
    "Savings"
  ]
}
```

### Change Currency
Living outside the US?

**In `user-defaults.json`:**
```json
{
  "currency": "eur"
}
```

### Set Billing Cycle
If your credit card bill starts on the 15th:

**In `user-defaults.json`:**
```json
{
  "startDate": 15
}
```

---

## 🔒 What's Safe to Edit?

### ✅ **100% Safe - Edit Freely:**
- `.env` file (all settings)
- `user-defaults.json` file (all settings)

### ⚠️ **Don't Touch (unless you know what you're doing):**
- Files in `cmd/` directory
- Files in `internal/` directory
- `go.mod`, `go.sum`
- `Dockerfile`

---

## 🆘 Troubleshooting

### "Port already in use"
**Solution:** Change the `PORT` in `.env` to something else (e.g., `3000`, `8081`)

### "Can't find .env file"
**Solution:** Make sure you copied `.env.example` to `.env` in the root directory
```bash
cp .env.example .env
```

### Changes not taking effect?
**Solution:** Restart the app after changing configuration files
```bash
# Stop the app (Ctrl+C), then start again
docker-compose up
# OR
go run cmd/expenseowl/main.go
```

### Want to reset to defaults?
**Solution:** Delete your `data/` folder and restart the app. Your `user-defaults.json` settings will be applied fresh.

---

## 📝 Notes

- **First Run Only:** `user-defaults.json` only applies when the app starts for the first time with no existing data
- **After First Run:** Use the Settings page in the app (http://localhost:8080/settings) to change categories, currency, etc.
- **Data Location:** Your expense data is stored in the `data/` folder (or wherever you set `STORAGE_URL`)
- **Backups:** The `data/` folder contains your expenses. Back it up regularly!

---

## 🎯 Summary

1. **Copy** `.env.example` to `.env`
2. **Edit** `.env` and `user-defaults.json` as needed (or keep the defaults)
3. **Start** the app
4. **Use** the Settings page for future changes

That's it! You now have full control over your ExpenseOwl configuration in two simple files. 🎉
