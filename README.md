# java-filmorate-schema

## Description

[Database schema](https://github.com/Stern-Ritter/java-filmorate-schema/blob/main/Schema.png)
[dbdiagram.io](https://dbdiagram.io/d/63cc2e09296d97641d7b34c4)

## Query examples

```java
#### public Film create(Film film)
```

```sql
INSERT INTO films (name, description, release_date, duration, age_rating_id)
VALUES (
'Гарри Поттер 20 лет спустя: Возвращение в Хогвартс',
'Актеры великой франшизы встречаются в школе магии. Архивные кадры, редкие интервью и ностальгическая атмосфера',
'2022-01-01',
99,
4
);
```

```java
#### public Film update(Film film)
```

```sql
UPDATE films SET (name, description, release_date, duration, age_rating_id) = (
'Гарри Поттер 20 лет спустя.',
'Актеры великой франшизы встречаются в школе магии.',
'2022-01-02',
120, 3)
WHERE film_id = 1;
```

```java
#### public Film get(long id)
```

```sql
SELECT film_id, name, description, release_date, duration, age_rating_id
FROM films
WEHERE film_id = 1;
```

```java
#### public List<Film> get()
```

```sql
SELECT film_id, name, description, release_date, duration, age_rating_id
FROM films;
```

```java
#### public Film addLike(long filmId, long userId)
```

```sql
INSERT INTO films_likes (film_id, user_id)
VALUES (1, 1);
```

```java
#### public Film deleteLike(long filmId, long userId)
```

```sql
DELETE FROM films_likes
WHERE filmId = 1 AND userId = 1;
```

```java
#### public List<Film> getPopular(int count)
```

```sql
SELECT film_id, name, description, release_date, duration, age_rating_id
FROM films
WHERE film_id IN (
SELECT filmId, COUNT(user_id)
FROM films_likes
ORDER BY COUNT(user_id) DESC
LIMIT 10
);
```

```java
#### public User create(User user)
```

```sql
INSERT INTO users (email, login, name, birthday)
VALUES (
'fadeew.k@mail.ru',
'Stern-Ritter',
'Konstantin',
'1992-04-28'
);
```

```java
#### public User update(User user)
```

```sql
UPDATE users SET (email, login, name, birthday) = (
'fadeew.ka@mail.ru',
'Kayen',
'Kostya',
'1992-04-27')
WHERE user_id = 1;
```

```java
#### public User get(long id)
```

```sql
SELECT user_id, email, login, name, birthday
FROM users
WEHERE user_id = 1;
```

```java
#### public List<User> get()
```

```sql
SELECT user_id, email, login, name, birthday
FROM users;
```

```java
#### public User addFriend(long userId, long otherUserId)
```

```sql
INSERT INTO users_friends (user_id, friend_id, boolean)
VALUES (1, 2, true);
```

```java
#### public User deleteFriend(long userId, long otherUserId)
```

```sql
DELETE FROM users_friends
WHERE userId = 1 AND otherUserId = 2;
```

```java
#### public List<User> getCommonFriends(long userId, long otherUserId)
```

```sql
SELECT user_id, email, login, name, birthday
FROM users as u
INNER JOIN users_friends as uf
ON u.user_id = uf.friend_id
AND uf.user_id = 1
INNER JOIN users_friends as ff
ON u.user_id = ff.friend_id
AND ff.user_id = 2;2
```

```java
#### public List<User> getFriends(long userId)
```

```sql
SELECT user_id, email, login, name, birthday
FROM users
WHERE user_id IN (
SELECT friend_id
FROM users_friends
WHERE user_id = 1
);
```
