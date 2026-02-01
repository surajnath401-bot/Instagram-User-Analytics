
# 📊 Instagram User Analytics (SQL Project)

## 📝 Project Overview

**Project Title:** Instagram User Analytics

This project focuses on analyzing **Instagram user behavior** using **SQL** to extract meaningful business insights.
As a **Data Analyst**, the goal is to help **product, marketing, and investor teams** make data-driven decisions by analyzing user engagement, activity, and platform usage.

The analysis is performed using **MySQL** and executed in **MySQL Workbench**.

---

## 🎯 Objectives

* Analyze user engagement and activity on Instagram
* Identify loyal and inactive users
* Support marketing and ad campaign decisions
* Provide key metrics for investors
* Detect potential bot or fake accounts

---

## 🛠️ Tools & Technologies

* **Database:** MySQL
* **Query Language:** SQL
* **Environment:** MySQL Workbench

**Concepts Used:**

* Joins
* Subqueries
* Aggregate Functions
* GROUP BY & HAVING
* Date Functions

---

## 📌 A) Marketing Analysis

### 1️⃣ Find the Five Oldest Instagram Users

```sql
SELECT *
FROM users
ORDER BY created_at
LIMIT 5;
```

---

### 2️⃣ Identify Users Who Have Never Posted a Photo

```sql
SELECT *
FROM users
LEFT JOIN photos 
ON users.id = photos.user_id
WHERE photos.user_id IS NULL;
```

---

### 3️⃣ Find the Contest Winner (Most Likes on a Single Photo)

```sql
SELECT 
    users.username,
    photos.id,
    photos.image_url,
    COUNT(likes.user_id) AS total_likes
FROM photos
INNER JOIN likes ON likes.photo_id = photos.id
INNER JOIN users ON photos.user_id = users.id
GROUP BY photos.id
ORDER BY total_likes DESC
LIMIT 1;
```

---

### 4️⃣ Find Top 5 Most Commonly Used Hashtags

```sql
SELECT 
    tags.tag_name,
    COUNT(*) AS total_tags
FROM photo_tags
JOIN tags ON photo_tags.tag_id = tags.id
GROUP BY tags.id
ORDER BY total_tags DESC
LIMIT 5;
```

---

### 5️⃣ Find the Day with Maximum User Registrations

```sql
SELECT 
    DAYNAME(created_at) AS day,
    COUNT(*) AS total_reg
FROM users
GROUP BY day
ORDER BY total_reg DESC
LIMIT 1;
```

---

## 📌 B) Investor Metrics

### 1️⃣ Average Number of Posts Per User

```sql
SELECT 
    (SELECT COUNT(*) FROM photos) / 
    (SELECT COUNT(*) FROM users) AS avg_posts_per_user;
```

---

### 2️⃣ Identify Users Who Liked Every Photo (Potential Bots)

```sql
SELECT 
    user_id,
    COUNT(*) AS total_likes
FROM likes
GROUP BY user_id
HAVING total_likes = (SELECT COUNT(*) FROM photos);
```

---

### 3️⃣ Find Usernames Who Liked Every Photo

```sql
SELECT 
    users.username,
    COUNT(*) AS total_likes
FROM users
JOIN likes ON users.id = likes.user_id
GROUP BY users.id
HAVING total_likes = (SELECT COUNT(*) FROM photos);
```

---

## 📌 Conclusion

In this project, SQL was used to analyze **Instagram user behavior** from both **marketing and investor perspectives**. By querying user, photo, like, and hashtag data, meaningful insights were extracted to support **business decision-making**.

### 🔍 Key Outcomes

* Identified **loyal and long-term users** for reward campaigns
* Detected **inactive users** for re-engagement strategies
* Determined **contest winners** using engagement metrics
* Found **popular hashtags** for brand and content strategy
* Analyzed **user registration trends** for ad scheduling
* Measured **user engagement levels**
* Identified **potential bot or fake accounts**

### 📈 Business Impact

* Improved marketing targeting and engagement
* Better understanding of active vs inactive users
* Increased investor confidence through transparency
* Data-driven support for platform growth strategies
