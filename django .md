---
title: "django "
tags: []
---

1 create a new project named boutique.
2 go to terminal and tape pip install django.

3 create a new project of django use this command:

 <django-admin startproject boutique .>
    # . veut dire que je veut l'installer a cette     endroit la (current folder)
    # boutique est le nom de mon projet
    
4-in the section folder we have .
        #<urls.py> ce fichier vas contenire le code qui contient le visuele ce que le user voit
            exemple #<home/acceuil/inscription>
        #<settings.py> est un module qui auras quellque paramatre pour notre application
        #<manage.py> sera utiliser pour lancer notre application web

5- lancer la commande python manage.py runserver .
        #<cette commande permet de lancer le serveur                    web equivalant a appache tomcat >
    #cette commande vas generer cette ligne 
             http://127.0.0.1:8000/

            #<qui le lien pour notre site web> 

6-pour cree sa premier application lancer la commade.
        #<python manage.py startapp wallpapers>

        contient les scriptes suivant 
        #<admin.py> espace administrateur
        #<apps.py> vas contenire un enssemble de 
    configuration pour note site web
        #<models.py> pour notre cas il s'agit d'une boutique donc il vas contenire comme exemple categorie prix etc
        #<views.py> ce que l'utilisateur voit quand il navigue entre les pages
        
    
7-the views function in #<views.py> sera utilise pour #<naviguer> entre les fentre donc si je vais dans  #<home/boutique> django vas envoyer une #<https request> au serveur pour faire apparaitre la page indique.

8-cree une premier vue de notre application web 
    donc faire ceci dans le script #<views.py>
############### VEIWS.PY ##########################    
    #<from django.shortcuts import render
from django.http import HttpResponse#reponse a une requete http>

    #<def index(request):
    return HttpResponse(hello world)>
    
###################################################
    
9- cree un script python nomer urls.py.
    et faire correspondre une url a #<def index>
############## URLS.PY wallappers ############
    #<from django.urls import path
from . import views
urlpatterns = [
           path('', views.index)#this means the root so /boutique
  ]>
    
###############################################
    
10- maintenant il faut declarer cette url dans le main project qui est boutique pour que django reconnaisse cette url donc :
#################### URLS.PY #####################
    #<from django.contrib import admin
    from django.urls import path,include
           
    urlpatterns = [
    path('admin/', admin.site.urls),
    path('wallpaper/', include('wallpapers.urls'))>

##################################################

11- create a model (order, customer , shopping card etc ).
    
    
    from django.db import models

# Create your models here.
#MODEL.MODEL CONTIENT DES MODULE NECESSAIRE COMME LES BASES DE DONN2E
#c'est comme tkinter qui contient des widget

#<class Wallpapers(models.Model):
    author = models.CharField(max_length=255)
    price = models.FloatField()
    contite = models.IntegerField()
    image = models.CharField(2083)
>
    
    
    https://www.google.com/url?sa=i&url=https%3A%2F%2Fpixabay.com%2Fimages%2Fsearch%2Fwallpaper%2F&psig=AOvVaw0Zuks4BxJp9aF4oHE1nAaL&ust=1612266051986000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCKCv4cLNyO4CFQAAAAAdAAAAABAS
    
    
    https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.pinterest.com%2Fpin%2F458663543303636653%2F&psig=AOvVaw0Zuks4BxJp9aF4oHE1nAaL&ust=1612266051986000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCKCv4cLNyO4CFQAAAAAdAAAAABAY
    
    
    https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.amazon.com%2FGamesHM-girly-wallpaper%2Fdp%2FB089Q3R68X&psig=AOvVaw0Zuks4BxJp9aF4oHE1nAaL&ust=1612266051986000&source=images&cd=vfe&ved=0CAIQjRxqFwoTCKCv4cLNyO4CFQAAAAAdAAAAABAf

###############################################

12-  maintenant il faut cree ca base de donnée
    ici pas la peine de la cree manualement car django peut la cree automatiquement avec ces etapes qui suivent.
    
    #<A> aller dans boutique => apps.py et copier le nom de la class donc #<WallpapersConfig>
    
    #<B> aller dans boutique=> settings.py et se rendre a la partie #<INSTALLED_APPS > et ajouter
cette ligne 
    #'wallpapers.apps.WallpapersConfig' 
    
    #<C> aller dans terminal et executer cette command #<python manage.py makemigrations> pour cree la table de le base de donnée
    
    #<D> pour finaliser et placer la table a db.sqlite3 on execute cette command 
        #<python manage.py migrate>
    create promotion si vous voullez


13- travailler avec le script admin.py.
    
    #create a superuser
        #<python manage.py createsuperuser>

14- ajouter les modeles a notre page admin .
    
    #<from django.contrib import admin
    from .models import Wallpapers
    # Register your models here.
    admin.site.register(Wallpapers) >

15- costumiser la page admin
    #afficher comme column tel un treeview.
    
    #<from django.contrib import admin
from .models import Wallpapers

# Register your models here.

class WallpapersAdmin(admin.ModelAdmin):
    list_display = ('author', 'price', 'contite')


admin.site.register(Wallpapers, WallpapersAdmin)
>

###########################################


16- Templates (designs)- the views.py est l'interface utilisateur ce que le user voit
    donc on vas ecrire notre code a cette endroit
    la
    
    def index(request):
    wall=Wallpapers.objects.all()#recuperer touts les element de notre base de donnée
    return render(request, 'index.html',
                  {'MyWallpapers': wall})

17- cree un package templates dans wallpapers
    qui vas contenure notre index.htlm
    
    <h1>produit</h1>

<ul>
    {% for items in MyWallpapers%}
        <li>{{ items.author}} {{ items.price}} $</li>
    {% endfor %}

</ul>
    

18- aller sur bootstrap et copier une base template
    
19- deplacer le fichier base.html dans un folder templates en dehors de lapplication 
    et l'ajouter dans settings avec cette command
    os.path.join(Base_dir, 'templates')
