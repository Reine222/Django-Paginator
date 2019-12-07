# Django-Paginator
pagination en Django
# Dans la vue ecrire le code suivant
# Exemple 1
# soit la table Post 
      from django.shortcuts import render
      from blog.models import Post
      from django.core.paginator import Paginator # < Import the Paginator class

      def home(request):

          posts = Post.objects.all()
          paginator = Paginator(posts, 3) # < 3 is the number of items on each page
          page = request.GET.get('page') # < Get the page number

          posts = paginator.get_page(page) # < New in 2.0!

          return render(request, 'base/home.html', {'posts': posts})
# Dans le template , dans la page correspondante ,ecrire le code suivant 

      <div class="pagination">

        {% if posts.has_previous %} // precedent
        <a href="?page=1">First</a>
        <a href="?page={{ posts.previous_page_number }}">Previous</a>
        {% endif %}

        <span>{{ posts.number }}</span> // numero de la page actuelle
        <span">of</span>
        <span>{{ posts.paginator.num_pages }}</span>  // numero de la page qui suit

        {% if posts.has_next %} // suivant
        <a href="?page={{ posts.next_page_number }}">Next</a> 
        <a href="?page={{ posts.paginator.num_pages }}">Last</a>
        {% endif %}
      </div>

# Exemple 2

# soit la table Post 
      from django.shortcuts import render
      from blog.models import Post
      from django.core.paginator import Paginator # < Import the Paginator class

      def home(request):

          posts = Post.objects.all()
          paginator = Paginator(posts, 3) # < 3 is the number of items on each page
          page = request.GET.get('page') # < Get the page number

          posts = paginator.get_page(page) # < New in 2.0!

          return render(request, 'base/home.html', {'posts': posts})

# Dans le template , dans la page correspondante ,ecrire le code suivant 

      <div class="pagination">

        {% if posts.has_previous %} // precedent
        <a href="?page={{ posts.previous_page_number }}">Previous</a>
        {% endif %}

        <span>{{ posts.number }}</span> // numero de la page actuelle
        <span">of</span>

        {% if posts.has_next %} // suivant
        <a href="?page={{ posts.next_page_number }}">Next</a> 
        {% endif %}
      </div>
      
