# ZSync - Quick Start Guide

A system that automatically tags and tracks execution metrics from CSV files.

## 🚀 How to Run This Project

### Step 1: Open Terminal
Open your terminal and navigate to the project folder:
```bash
cd /Users/ricknysanon/Documents/zinnia/zinniasync
```

### Step 2: Create Environment File
Create a `.env` file in the project root:
```bash
echo 'DATABASE_URL="postgresql://zsync_user:zsync_password@localhost:5432/zsync_db?schema=public"' > .env
```

### Step 3: Start the Database
```bash
docker-compose up -d
```

### Step 4: Set Up Database Tables and Data
```bash
npx prisma generate
npx prisma migrate dev --name init
npx prisma db seed
npm run seed:analytics  # Important: This seeds the analytics dashboard data
```

### Step 5: Start the Application
```bash
npm run dev
```

### Step 6: Open in Browser
Go to: http://localhost:3000

## 📱 Using the Application

### Upload CSV Files
1. Click "Upload" in the navigation
2. Select a category (e.g., Engineering, Call Center)
3. Drag and drop your CSV file
4. Click "Upload Data"

### View Dashboard
1. Click "Dashboard" in the navigation
2. See your metrics with automatic tags:
   - ✅ On-time (green)
   - ⚠️ Delayed (red)
   - 🔄 In-progress (blue)
   - ❌ Incomplete (orange)

## 🛑 Stopping the Application

1. Press `Ctrl+C` in the terminal to stop the app
2. Run `docker-compose down` to stop the database

## 📊 Sample CSV Format

### Engineering CSV Example:
```
Task_ID,Description,Planned_Date,Actual_Date,Status
ENG-001,Build login feature,2024-01-15,2024-01-14,Completed
ENG-002,API integration,2024-01-20,2024-01-22,Completed
ENG-003,Dashboard UI,2024-01-25,,In Progress
```

### Call Center CSV Example:
```
Agent_ID,Target_Date,Achievement_Date,Total_Calls_T,Call_Quality_Type
A001,2024-01-15,2024-01-15,150,FCR
A002,2024-01-16,,120,Service Level
```

## ❓ Troubleshooting

**Database won't start?**
- Make sure Docker Desktop is running
- Check if port 5432 is already in use

**Can't access the app?**
- Make sure you ran `npm run dev`
- Check if another app is using port 3000

**Need to reset everything?**
```bash
docker-compose down -v
npx prisma migrate reset
npx prisma db seed
```

## 📝 Notes
- The app automatically tags your metrics based on dates
- Green = On-time, Red = Delayed, Blue = In Progress, Orange = Incomplete
- Export your data anytime from the Dashboard
