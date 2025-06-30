# Social-media-platform-
from django.apps import AppConfig

class SocialAppConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'socialapp'
"""

# socialapp/models.py
models_py = """
from django.db import models
from django.contrib.auth.models import User

class Post(models.Model):
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

class Comment(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)

class Like(models.Model):
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
    user = models.ForeignKey(User, on_delete=models.CASCADE)
"""

# socialapp/views.py
views_py = """
from django.shortcuts import render
from django.contrib.auth.decorators import login_required
from .models import Post

@login_required
def home(request):
    posts = Post.objects.all().order_by('-created_at')
    return render(request, 'socialapp/home.html', {'posts': posts})
"""

# socialapp/urls.py
app_urls_py = """
from django.urls import path
from . import views

urlpatterns = [
    path('', views.home, name='home'),
]
"""

# templates/socialapp/home.html
home_html = """
<h1>Social Media Feed</h1>
{% for post in posts %}
  <div>
    <p><strong>{{ post.author.username }}</strong>: {{ post.content }}</p>
  </div>
{% endfor %}
"""
