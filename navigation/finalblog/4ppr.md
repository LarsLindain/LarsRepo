---
layout: page
title: Tri 2 PPR Blog
permalink: /ppr
---

<h1> Personalized Project Reference (PPR) - BinaryOverflow Blog</h1>

<h2>Introduction</h2>
<p>For my <strong>Create Performance Task (CPT)</strong>, I developed the <strong>BinaryOverflow Blog</strong>, a community-driven website where users can create and interact with posts. This project involved <em>full-stack development</em>, including frontend, backend, authentication, and API integration.</p>

<p>As part of my <strong>PPR submission</strong>, I will be highlighting:</p>
<ul>
    <li><strong>A List (Data Structure)</strong> - Used to store blog posts.</li>
    <li><strong>A Procedure (Function) that Manipulates the List</strong> - Retrieves posts for frontend display.</li>
</ul>

<hr>

<h2> List - Storing Blog Posts</h2>

<h3>User Management Screenshot</h3>
<!-- Replace with the actual URL of your screenshot -->
<img src="https://i.postimg.cc/Bv8qq6L8/Screenshot-2025-03-03-at-3-24-25-AM.png" alt="Backend Pic" width="600">

<pre>
<code>
class BinaryOverflowContent(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    _title = db.Column(db.String(255), nullable=False)
    _author = db.Column(db.Integer, db.ForeignKey('users.id'), nullable=False)
    _date_posted = db.Column(db.DateTime, nullable=False, default=datetime.now(timezone.utc))
    _content = db.Column(db.String(255), nullable=False)
</code>
</pre>

<h3>Explanation</h3>
<ul>
    <li>This is the <strong>database model</strong> for blog posts.</li>
    <li>It <strong>stores and organizes</strong> posts submitted by users.</li>
    <li><strong>Key elements:</strong>
        <ul>
            <li><code>id</code> - Unique identifier for each post.</li>
            <li><code>title</code> - The title of the blog post.</li>
            <li><code>user_id</code> - Connects each post to the author.</li>
            <li><code>content</code> - Stores the actual post text.</li>
            <li><code>date_posted</code> - Establishes a <em>relationship</em> between posts and their publish date.</li>
        </ul>
    </li>
</ul>

<hr>

<h2> Procedure - Retrieving Posts for Frontend</h2>

<h3>Code Screenshot</h3>
<!-- Replace with the actual URL of your screenshot -->
<img src="https://i.postimg.cc/qMJCq7pK/Screenshot-2025-03-10-at-11-18-05-PM.png" alt="Post Retrieval Procedure Screenshot" width="700">

<pre>
<code>
class fetch_frontend(Resource):
    def get(self):
        posts = BinaryOverflowContent.query.all()
        json_ready = [post.read() for post in posts]
        return json_ready
</code>
</pre>

<h3>Explanation</h3>
<ul>
    <li>The function <code>fetch_frontend()</code> retrieves all blog posts from the database.</li>
    <li>It <strong>queries the database</strong>, retrieves stored posts, and <strong>converts them into a JSON format</strong> for easy use in the frontend.</li>
    <li><strong>How It Works:</strong>
        <ol>
            <li>Calls <code>query.all()</code> to fetch all stored posts.</li>
            <li>Uses list comprehension <code>[post.read() for post in posts]</code> to convert the data into a <em>structured format</em>.</li>
            <li>Returns the processed posts in <strong>JSON format</strong>.</li>
        </ol>
    </li>
</ul>

<h3>How This Improves the Program</h3>
<ul>
    <li><strong>Abstraction:</strong> Instead of manually fetching posts everywhere, this function <em>simplifies</em> data retrieval into <strong>one reusable function</strong>.</li>
    <li><strong>Efficiency:</strong> Converting posts into JSON ensures <strong>fast frontend rendering</strong>.</li>
    <li><strong>Scalability:</strong> New posts <em>automatically appear</em> on the frontend without additional logic.</li>
</ul>

<hr>

<h2> Challenges & Future Improvements</h2>
<ul>
    <li><strong>Authentication Bugs:</strong> Originally, users could post without being logged in. I fixed this by requiring <strong>JWT authentication</strong>.</li>
    <li><strong>Post Update:</strong> After posting, you need to reload the page to see your post. In the future, I will implement another GEt function built in so there is no need to reload.</li>
</ul>

<hr>

<h2> Conclusion</h2>
<p>Completing the <strong>BinaryOverflow Blog</strong> helped me develop strong <em>full-stack skills</em>, including <strong>database management, API integration, and frontend optimization</strong>. This PPR has helped me reflect on how <strong>lists and procedures</strong> play a crucial role in managing <em>large-scale web applications</em>.</p>


<h2> MCQ Recap</h2>

<p>After taking the Tri 2 MCQ I would say I have made progress since the previous MCQ done eariler this trimester, but am I not where I want to be by the end of the year.</p>

<img src="https://i.postimg.cc/9MW80257/Screenshot-2025-03-03-at-10-11-44-AM.png" alt="MCQ score" width="600">

<img src="https://i.postimg.cc/RZKXThvt/Screenshot-2025-03-03-at-10-15-58-AM.png" alt="MCQ Breakdown" width="600">

<h3>Worst topic rates</h3>

<p><strong> Identifying and Correcting Errors</strong> was my lowest preforming topic.</p>

<img src="https://i.postimg.cc/QVG34HCN/Screenshot-2025-03-11-at-12-34-51-AM.png" alt="EX q1" width="600">

<img src=" https://i.postimg.cc/JnxxYghs/Screenshot-2025-03-11-at-12-36-28-AM.png" alt="Ex q2" width="600">

<p> To improve on this topics, I will study how to break down and analyze code blocks and find how why they would/ would not work. Example such as the question above that I had gotten wrong would help as they not only show the correct answer, but also state why the chosen answer was incorrect and what it would change instead.</p> 