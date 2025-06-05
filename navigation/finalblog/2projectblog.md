---
layout: page
title: Tri 3 Final Blog Continue..(2)
permalink: /finalblog2
---

<h2> Project Demo + Blog</h2>

<h3>Binary Overflow Demo</h3>

<p> After logging in a user can add a title and content, then click post to send the data to the backend to be save and displayed dynamically. Once sent, the user can reload to find their post as well as other posts made by users on the platform.</p>

<img src="https://i.postimg.cc/SKcWtyS9/Screenshot-2025-03-03-at-3-24-00-AM.png" alt="Frontend Post" width="600">

<img src="https://i.postimg.cc/Bv8qq6L8/Screenshot-2025-03-03-at-3-24-25-AM.png" alt="Backend Pic" width="600">

<p> Alongside posting, users are able to update posts by upvoting and downvoting other posts to show their approval or disapprove of the post. Users with access (such as the original author or an admin) can also delete posts off the site.</p>

<h3>CPT Concepts</h3>

<p>Algorithm: Fetch Frontend Function- The Get method is used to fetch all posts from the database; The Post method requires authtification to create posts.</p>

```javascript
class BinaryOverflowPostAPI:
    # Fetches data for Frontend to build
    class fetch_frontend(Resource):
        def get(self):
            """Fetch all posts from the database."""
            posts = BinaryOverflowContent.query.all()
            json_ready = [post.read() for post in posts]
            return json_ready
        
        @token_required()
        def post(self):
            """Create a new post."""
            current_user = g.current_user
            data = request.get_json()
            post = BinaryOverflowContent(data["title"], current_user.id, data["content"])
            post.create()
            return jsonify(post.read())
```
<p>Management: SQLAlchemy database - Using BinaryOverflowContent, it stores user generated posts with data including, titles, content, and user data</p>

```javascript
from flask_sqlalchemy import SQLAlchemy

db = SQLAlchemy()

class BinaryOverflowContent(db.Model):
    """Database model for storing user posts."""
    id = db.Column(db.Integer, primary_key=True)
    title = db.Column(db.String(255), nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)
    content = db.Column(db.Text, nullable=False)
    upvotes = db.Column(db.Integer, default=0)
    downvotes = db.Column(db.Integer, default=0)

    def create(self):
        """Save the post to the database."""
        db.session.add(self)
        db.session.commit()

    def read(self):
        """Return post data as a dictionary."""
        return {
            "id": self.id,
            "title": self.title,
            "user_id": self.user_id,
            "content": self.content,
            "upvotes": self.upvotes,
            "downvotes": self.downvotes
        }
```

<h3>N@tM Feedback</h3>

<p> Night at the Mueseum was a very fun night a was able to see many other groups' hard work over the past dozen weeks. I was also able to present and showcase my work, able to get complements and contrustive criticism.</p>

<h4> Glows </h4>
- Engaging presentation
- Each page and feature was cohesive
- The features were interesting and interactive 

<h4>Grows </h4>
- The titles of our features could better connect with the features itself
- The pages seemed a little bland, the frontend could use work

<h3>MCQ</h3>

<p>After taking the Tri 2 MCQ I would say I have made progress since the previous MCQ done eariler this trimester, but am I not where I want to be by the end of the year.</p>

<img src="https://i.postimg.cc/9MW80257/Screenshot-2025-03-03-at-10-11-44-AM.png" alt="MCQ score" width="600">

<img src="https://i.postimg.cc/RZKXThvt/Screenshot-2025-03-03-at-10-15-58-AM.png" alt="MCQ Breakdown" width="600">

<td><a href="/LarsRepo/finalblog3" class="button">Continue to Retrospecitive