
<!DOCTYPE html>
<html lang="fr-fr">
<head>
  <meta charset="utf-8" />
<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
<meta name="viewport" content="width=device-width, initial-scale=1.0">


  <meta name="description" content="Mettre en page un site statique avec Jekyll et Github Pages

Choisir un thème officiel compatible Github page

Github pages propose une liste de thèmes compatibles à l’adresse :
+https://pages.github.com/themes/
Afin de les utiliser, il faut suivre la procédure d’installation indiqué à l’adresse du dépot du theme choisi.

Dans notre cas, nous choisissons le theme tactile (un thème sobre et responsive) :

Installation du thème


  Ouvrir le fichier “_config.yml” à la racine de votre site et ajouter le nom du thème :


theme: jekyll-theme-tactile


  Pour que le thème soit actif aussi en local, vous pouvez modifier le “.gemfile”, en ajoutant : gem "github-pages", group: :jekyll_plugins, puis lancer
    bundle update github-pages

  
  Il faut enfin ajouter ou modifier le fichier “_layouts/default.html” en faisant un copier/coller du template présent sur le dépot en ligne d thèmé choisit.
Dans notre cas :https://github.com/pages-themes/tactile/blob/master/_layouts/default.html
  Le push une fois effectué, la page rafraichie et l’historique effacé, le nouveau thème devrait actif!


Remarques :


  
    Si le thème précédent était ‘minima’, le thème par défaut chargé à la création du site, ces procédures ne sont pas suffisantes.

    
      Il faudra aussi effacer toute les références à “minima”, que ce soit dans le config.yml, about.md et gemfile.
      Il faudra aussi modifier les premières lignes de tous les articles et pages déja écrites en remplacant layout: post par layout: default
    
  


On remarquera alors que la page d’accueil n’affiche plus les liens vers les articles, comme pouvez le faire minima. Nous allons voir par la suite, comment mettre en page son site et récupérer boutons et fonctionnalités.

Ajouter une barre de navigation (navbar)

https://www.taniarascia.com/responsive-dropdown-navigation-bar/

Créer un barre de navigation avancée

https://learn.cloudcannon.com/jekyll/advanced-navigation/

Il va falloir créer un fichier “navigationTree.yml” qui va nous permettre d’ordonner les pages dans le menu.
Ainsi à la racine du site :

mkdir -p _data
nano navigationTree.yml


On integre ensuite la liste des pages de notre site telle que :
- link: /
  name: Home
- link: /about/
  name: About
- link: /services
  name: Services


Puis dans le fichier _includes/navigation.html ( créé précédement pour la barre de navigation “simple” ), il faut insérer les lignes suivantes ;

 {% for item in site.data.navigation %}
    &lt;a href="{{ item.link %}" {% if item.link == page.url %}class="active"{% endif %}&gt;
      {{ item.name }}
    &lt;/a&gt;
  {% endfor %}




Personnaliser la page d’accueil d’un site statique sous Jekyll
Le contenu de la page d’accueil se situe dans le fichier index.md

Afficher les derniers articles

Créer une nouvelle Page
Pour créer une nouvelle page, il suffit de copier la page “about.md” et de la renommée.
Toutes les nouvelles pages doivent etre enregistrées à la racine du site.

Comment ajouter un sommaire ( TOC : Table of Content)
Avec krawdow sous github pages, il faut inserer dans l’article :
* TOC
{:toc}

Résultat :


  Mettre en page un site statique avec Jekyll et Github Pages    
      Choisir un thème officiel compatible Github page        
          Installation du thème
        
      
      Ajouter une barre de navigation (navbar)
      Créer un barre de navigation avancée
      Afficher les derniers articles
      Créer une nouvelle Page
      Comment ajouter un sommaire ( TOC : Table of Content)
      Comment ajouter une image
      Comment insérer un lien vers une autre page de son site
      Comment insérer un bout de code sur une ligne
      Personnaliser le template avec Bootstrap        
          Installer Bootstrap pour Jekyll
        
      
      Messages d’erreur:        
          The jekyll-theme-minimal theme could not be found
          Error:  Could not locate the included file ‘icon-github.html’
        
      
      Liens
    
  


Comment ajouter une image

![titre image](http://memofil.github.io/assets/image.png)

Comment insérer un lien vers une autre page de son site
Exemple d’un lien qui pointe vers cet article :
[--&gt; Mettre en page un site satique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %})


Résultat : Mettre en page un site statique

Comment insérer un bout de code sur une ligne
Pour avoir index.htlm , il faut entourer le mot par le caractère `, tel que :

`index.html`


Personnaliser le template avec Bootstrap

Installer Bootstrap pour Jekyll
Boostrap fonctionne nativement avec less, pour utiliser Bootstrap avec Jekyll qui utilise Sass, on doit installer Bootstrap-sass via les gem Ruby :


  Install le gem bootstrap-sass :


sudo gem install bootstrap-sass



  Se rendre à la racine du site jekyll et  ajouter les lignes suivantes au fichier Gemfile  :
    gem 'bootstrap-sass', '~&gt; 3.3.7'
gem 'sass-rails', '&gt;= 3.2'
    
  
  Afin de réinitialiser la configuration du site jekyll ,  taper :


bundle install


  
    Créer un répertoire _sass à la racine du site ou seront stocké les templates .scss de Bootstrap
  
  
    Télécharger le dépot bootstrap afin d’y récupérer les éléments necessaires à Jekyll pour pouvoir compiler les styles bootstrap. On déplacera alors le dossier assets/stylesheets/bootstrap et le fichier assets/stylesheets/_bootstrap.scss dans le dossier _sass tout juste créé.
  
  
    Modifier le ‘_config.yml’ en y ajoutant les lignes  (docs jekyll):
  


sass:
    sass_dir: _sass


Messages d’erreur:

The jekyll-theme-minimal theme could not be found
En tentant d’exécuter en local Jekyll avec la commande
bundle exec jekyll serve

On obtient
jekyll 3.4.3 | Error:  The jekyll-theme-minimal theme could not be found


Le thème est manquant. Il faut ajouter gem "jekyll-theme-minimal", "~&gt; 0.0.3" au Gemfile et l’installer:
bundle install


Error:  Could not locate the included file ‘icon-github.html’

En tentant d’exécuter en local Jekyll avec la commande
bundle exec jekyll serve

On obtient
bundle exec jekyll serve
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
            Source: /home/demiton/git/demiton.github.io
       Destination: /home/demiton/git/demiton.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
     Build Warning: Layout 'post' requested in _posts/2017-06-06-welcome-to-jekyll.markdown does not exist.
  Liquid Exception: Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source. in about.md
jekyll 3.4.3 | Error:  Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source.


Le fichier ‘icon-github.html’ est introuvable, ce dernier est associé au theme minima qui est probablement non installé :

bundle install minima


Liens

  http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming
  http://veithen.github.io/2015/03/26/jekyll-bootstrap.html
  https://simpleit.rocks/how-to-add-bootstrap-4-to-jekyll-the-right-way/
  https://blog.webjeda.com/jekyll-categories/
  http://longqian.me/2017/02/09/github-jekyll-tag/
  https://css-tricks.com/snippets/css/a-guide-to-flexbox/
  https://www.w3schools.com/css/css3_flexbox.asp

" />
  <meta property="og:description" content="Mettre en page un site statique avec Jekyll et Github Pages

Choisir un thème officiel compatible Github page

Github pages propose une liste de thèmes compatibles à l’adresse :
+https://pages.github.com/themes/
Afin de les utiliser, il faut suivre la procédure d’installation indiqué à l’adresse du dépot du theme choisi.

Dans notre cas, nous choisissons le theme tactile (un thème sobre et responsive) :

Installation du thème


  Ouvrir le fichier “_config.yml” à la racine de votre site et ajouter le nom du thème :


theme: jekyll-theme-tactile


  Pour que le thème soit actif aussi en local, vous pouvez modifier le “.gemfile”, en ajoutant : gem "github-pages", group: :jekyll_plugins, puis lancer
    bundle update github-pages

  
  Il faut enfin ajouter ou modifier le fichier “_layouts/default.html” en faisant un copier/coller du template présent sur le dépot en ligne d thèmé choisit.
Dans notre cas :https://github.com/pages-themes/tactile/blob/master/_layouts/default.html
  Le push une fois effectué, la page rafraichie et l’historique effacé, le nouveau thème devrait actif!


Remarques :


  
    Si le thème précédent était ‘minima’, le thème par défaut chargé à la création du site, ces procédures ne sont pas suffisantes.

    
      Il faudra aussi effacer toute les références à “minima”, que ce soit dans le config.yml, about.md et gemfile.
      Il faudra aussi modifier les premières lignes de tous les articles et pages déja écrites en remplacant layout: post par layout: default
    
  


On remarquera alors que la page d’accueil n’affiche plus les liens vers les articles, comme pouvez le faire minima. Nous allons voir par la suite, comment mettre en page son site et récupérer boutons et fonctionnalités.

Ajouter une barre de navigation (navbar)

https://www.taniarascia.com/responsive-dropdown-navigation-bar/

Créer un barre de navigation avancée

https://learn.cloudcannon.com/jekyll/advanced-navigation/

Il va falloir créer un fichier “navigationTree.yml” qui va nous permettre d’ordonner les pages dans le menu.
Ainsi à la racine du site :

mkdir -p _data
nano navigationTree.yml


On integre ensuite la liste des pages de notre site telle que :
- link: /
  name: Home
- link: /about/
  name: About
- link: /services
  name: Services


Puis dans le fichier _includes/navigation.html ( créé précédement pour la barre de navigation “simple” ), il faut insérer les lignes suivantes ;

 {% for item in site.data.navigation %}
    &lt;a href="{{ item.link %}" {% if item.link == page.url %}class="active"{% endif %}&gt;
      {{ item.name }}
    &lt;/a&gt;
  {% endfor %}




Personnaliser la page d’accueil d’un site statique sous Jekyll
Le contenu de la page d’accueil se situe dans le fichier index.md

Afficher les derniers articles

Créer une nouvelle Page
Pour créer une nouvelle page, il suffit de copier la page “about.md” et de la renommée.
Toutes les nouvelles pages doivent etre enregistrées à la racine du site.

Comment ajouter un sommaire ( TOC : Table of Content)
Avec krawdow sous github pages, il faut inserer dans l’article :
* TOC
{:toc}

Résultat :


  Mettre en page un site statique avec Jekyll et Github Pages    
      Choisir un thème officiel compatible Github page        
          Installation du thème
        
      
      Ajouter une barre de navigation (navbar)
      Créer un barre de navigation avancée
      Afficher les derniers articles
      Créer une nouvelle Page
      Comment ajouter un sommaire ( TOC : Table of Content)
      Comment ajouter une image
      Comment insérer un lien vers une autre page de son site
      Comment insérer un bout de code sur une ligne
      Personnaliser le template avec Bootstrap        
          Installer Bootstrap pour Jekyll
        
      
      Messages d’erreur:        
          The jekyll-theme-minimal theme could not be found
          Error:  Could not locate the included file ‘icon-github.html’
        
      
      Liens
    
  


Comment ajouter une image

![titre image](http://memofil.github.io/assets/image.png)

Comment insérer un lien vers une autre page de son site
Exemple d’un lien qui pointe vers cet article :
[--&gt; Mettre en page un site satique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %})


Résultat : Mettre en page un site statique

Comment insérer un bout de code sur une ligne
Pour avoir index.htlm , il faut entourer le mot par le caractère `, tel que :

`index.html`


Personnaliser le template avec Bootstrap

Installer Bootstrap pour Jekyll
Boostrap fonctionne nativement avec less, pour utiliser Bootstrap avec Jekyll qui utilise Sass, on doit installer Bootstrap-sass via les gem Ruby :


  Install le gem bootstrap-sass :


sudo gem install bootstrap-sass



  Se rendre à la racine du site jekyll et  ajouter les lignes suivantes au fichier Gemfile  :
    gem 'bootstrap-sass', '~&gt; 3.3.7'
gem 'sass-rails', '&gt;= 3.2'
    
  
  Afin de réinitialiser la configuration du site jekyll ,  taper :


bundle install


  
    Créer un répertoire _sass à la racine du site ou seront stocké les templates .scss de Bootstrap
  
  
    Télécharger le dépot bootstrap afin d’y récupérer les éléments necessaires à Jekyll pour pouvoir compiler les styles bootstrap. On déplacera alors le dossier assets/stylesheets/bootstrap et le fichier assets/stylesheets/_bootstrap.scss dans le dossier _sass tout juste créé.
  
  
    Modifier le ‘_config.yml’ en y ajoutant les lignes  (docs jekyll):
  


sass:
    sass_dir: _sass


Messages d’erreur:

The jekyll-theme-minimal theme could not be found
En tentant d’exécuter en local Jekyll avec la commande
bundle exec jekyll serve

On obtient
jekyll 3.4.3 | Error:  The jekyll-theme-minimal theme could not be found


Le thème est manquant. Il faut ajouter gem "jekyll-theme-minimal", "~&gt; 0.0.3" au Gemfile et l’installer:
bundle install


Error:  Could not locate the included file ‘icon-github.html’

En tentant d’exécuter en local Jekyll avec la commande
bundle exec jekyll serve

On obtient
bundle exec jekyll serve
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
            Source: /home/demiton/git/demiton.github.io
       Destination: /home/demiton/git/demiton.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
     Build Warning: Layout 'post' requested in _posts/2017-06-06-welcome-to-jekyll.markdown does not exist.
  Liquid Exception: Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source. in about.md
jekyll 3.4.3 | Error:  Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source.


Le fichier ‘icon-github.html’ est introuvable, ce dernier est associé au theme minima qui est probablement non installé :

bundle install minima


Liens

  http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming
  http://veithen.github.io/2015/03/26/jekyll-bootstrap.html
  https://simpleit.rocks/how-to-add-bootstrap-4-to-jekyll-the-right-way/
  https://blog.webjeda.com/jekyll-categories/
  http://longqian.me/2017/02/09/github-jekyll-tag/
  https://css-tricks.com/snippets/css/a-guide-to-flexbox/
  https://www.w3schools.com/css/css3_flexbox.asp

" />

  <meta name="author" content="Mémofil" />


  <meta property="og:title" content="Mettre en page un site statique avec Jekyll et Github Pages" />
  <meta property="twitter:title" content="Mettre en page un site statique avec Jekyll et Github Pages" />
 

  <link href='https://fonts.googleapis.com/css?family=Chivo:900' rel='stylesheet' type='text/css'>
  <link rel="stylesheet" href="/assets/css/style.css?v=2c82ce55797de712883f96c16b46e3be4435b368">
  <link rel="stylesheet" type="text/css" href="/assets/css/print.css" media="print">
  <!--[if lt IE 9]>
  <script src="//html5shiv.googlecode.com/svn/trunk/html5.js"></script>
  <![endif]-->
  <script type="text/javascript" src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.0/jquery.min.js"></script>
  <title>Mémofil by Memofil</title>
</head>

  <body>
  
<section class="navigation">
  <div class="nav-container">
    <div class="brand">
    <ul>
    <li class="left">
    <figure>
   <a href="http://memofil.github.io">
   <img src="/logo.png" style="max-width: 50px;"
      alt="Memofil"/>
    </a>
   <figcaption></figcaption>
</figure>

      </li>
      <li class="right">
          <h1>Mémofil</h1>
          <h2>Notes pour retrouver le fil de ses idées</h2>
          
      </li>
      </ul>
      </div>
    <nav>
    <script type="text/javascript">(function($) { // Begin jQuery
  $(function() { // DOM ready
    // If a link has a dropdown, add sub menu toggle.
    $('nav ul li a:not(:only-child)').click(function(e) {
      $(this).siblings('.nav-dropdown').toggle();
      // Close one dropdown when selecting another
      $('.nav-dropdown').not($(this).siblings()).hide();
      e.stopPropagation();
    });
    // Clicking away from dropdown will remove the dropdown class
    $('html').click(function() {
      $('.nav-dropdown').hide();
    });
    // Toggle open and close nav styles on click
    $('#nav-toggle').click(function() {
      $('nav ul').slideToggle();
    });
    // Hamburger to X toggle
    $('#nav-toggle').on('click', function() {
      this.classList.toggle('active');
    });
  }); // end DOM ready
})(jQuery); // end jQuery</script>
   <!-- <script type="text/javascript" src="./_includes_scripts/navbar.js"></script>-->
      <div class="nav-mobile">
        <a id="nav-toggle" href="#!"><span></span></a>
      </div>
      
        <ul class="nav-list">
            <li>
            <a href="http://memofil.github.io">Home</a>
            </li>
            
             
            
            
            
            
            
            
            
            
            
            
            <li>
                <a href="/categories/">Catégories</a>
            </li>
            
            
            
            <li>
                <a href="/liens/">Liens</a>
            </li>
            
            
            
            <li>
                <a href="/archives/">Archives</a>
            </li>
            
            
      </ul>
    </nav>
   
  </div>
</section>
    <div id="container">
      <div class="inner">
        <section id="main_content">
          <h1 id="mettre-en-page-un-site-statique-avec-jekyll-et-github-pages">Mettre en page un site statique avec Jekyll et Github Pages</h1>

<h2 id="choisir-un-thème-officiel-compatible-github-page">Choisir un thème officiel compatible Github page</h2>

<p>Github pages propose une liste de thèmes compatibles à l’adresse :
+<a href="https://pages.github.com/themes/" target="_blank">https://pages.github.com/themes/</a>
Afin de les utiliser, il faut suivre la procédure d’installation indiqué à l’adresse du dépot du theme choisi.</p>

<p>Dans notre cas, nous choisissons le theme <a href="https://github.com/pages-themes/tactile" target="_blank"><strong>tactile</strong> (un thème sobre et responsive)</a> :</p>

<h3 id="installation-du-thème">Installation du thème</h3>

<ol>
  <li>Ouvrir le fichier “_config.yml” à la racine de votre site et ajouter le nom du thème :</li>
</ol>

<figure class="highlight"><pre><code class="language-ruby" data-lang="ruby"><span class="ss">theme: </span><span class="n">jekyll</span><span class="o">-</span><span class="n">theme</span><span class="o">-</span><span class="n">tactile</span></code></pre></figure>

<ol>
  <li>Pour que le thème soit actif aussi en local, vous pouvez modifier le “.gemfile”, en ajoutant : <code class="highlighter-rouge">gem "github-pages", group: :jekyll_plugins</code>, puis lancer
    <pre><code class="language-BASH">bundle update github-pages
</code></pre>
  </li>
  <li>Il faut enfin ajouter ou modifier le fichier “_layouts/default.html” en faisant un copier/coller du template présent sur le dépot en ligne d thèmé choisit.
Dans notre cas :<a href="https://github.com/pages-themes/tactile/blob/master/_layouts/default.html" target="_blank">https://github.com/pages-themes/tactile/blob/master/_layouts/default.html</a></li>
  <li>Le push une fois effectué, la page rafraichie et l’historique effacé, le nouveau thème devrait actif!</li>
</ol>

<p><strong>Remarques :</strong></p>

<ul>
  <li>
    <p>Si le thème précédent était ‘minima’, le thème par défaut chargé à la création du site, ces procédures ne sont pas suffisantes.</p>

    <ul>
      <li>Il faudra aussi effacer toute les références à “minima”, que ce soit dans le <code class="highlighter-rouge">config.yml</code>, <code class="highlighter-rouge">about.md</code> et <code class="highlighter-rouge">gemfile</code>.</li>
      <li>Il faudra aussi modifier les premières lignes de tous les articles et pages déja écrites en remplacant <code class="highlighter-rouge">layout: post</code> par <code class="highlighter-rouge">layout: default</code></li>
    </ul>
  </li>
</ul>

<p>On remarquera alors que la page d’accueil n’affiche plus les liens vers les articles, comme pouvez le faire minima. Nous allons voir par la suite, comment mettre en page son site et récupérer boutons et fonctionnalités.</p>

<h2 id="ajouter-une-barre-de-navigation-navbar">Ajouter une barre de navigation (navbar)</h2>

<p><a href="https://www.taniarascia.com/responsive-dropdown-navigation-bar/" target="_blank">https://www.taniarascia.com/responsive-dropdown-navigation-bar/</a></p>

<h2 id="créer-un-barre-de-navigation-avancée">Créer un barre de navigation avancée</h2>

<p><a href="https://learn.cloudcannon.com/jekyll/advanced-navigation/" target="_blank">https://learn.cloudcannon.com/jekyll/advanced-navigation/</a></p>

<p>Il va falloir créer un fichier “navigationTree.yml” qui va nous permettre d’ordonner les pages dans le menu.
Ainsi à la racine du site :</p>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>mkdir -p _data
nano navigationTree.yml
</code></pre></div></div>

<p>On integre ensuite la liste des pages de notre site telle que :</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>- link: /
  name: Home
- link: /about/
  name: About
- link: /services
  name: Services
</code></pre></div></div>

<p>Puis dans le fichier <code class="highlighter-rouge">_includes/navigation.html</code> ( créé précédement pour la barre de navigation “simple” ), il faut insérer les lignes suivantes ;</p>
<pre><code class="language-HTML">
 {% for item in site.data.navigation %}
    &lt;a href="{{ item.link %}" {% if item.link == page.url %}class="active"{% endif %}&gt;
      {{ item.name }}
    &lt;/a&gt;
  {% endfor %}


</code></pre>

<p>Personnaliser la page d’accueil d’un site statique sous Jekyll
Le contenu de la page d’accueil se situe dans le fichier <code class="highlighter-rouge">index.md</code></p>

<h2 id="afficher-les-derniers-articles">Afficher les derniers articles</h2>

<h2 id="créer-une-nouvelle-page">Créer une nouvelle Page</h2>
<p>Pour créer une nouvelle page, il suffit de copier la page “about.md” et de la renommée.
Toutes les nouvelles pages doivent etre enregistrées à la racine du site.</p>

<h2 id="comment-ajouter-un-sommaire--toc--table-of-content">Comment ajouter un sommaire ( TOC : Table of Content)</h2>
<p>Avec krawdow sous github pages, il faut inserer dans l’article :</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>* TOC
{:toc}
</code></pre></div></div>
<p>Résultat :</p>

<ul id="markdown-toc">
  <li><a href="#mettre-en-page-un-site-statique-avec-jekyll-et-github-pages" id="markdown-toc-mettre-en-page-un-site-statique-avec-jekyll-et-github-pages">Mettre en page un site statique avec Jekyll et Github Pages</a>    <ul>
      <li><a href="#choisir-un-thème-officiel-compatible-github-page" id="markdown-toc-choisir-un-thème-officiel-compatible-github-page">Choisir un thème officiel compatible Github page</a>        <ul>
          <li><a href="#installation-du-thème" id="markdown-toc-installation-du-thème">Installation du thème</a></li>
        </ul>
      </li>
      <li><a href="#ajouter-une-barre-de-navigation-navbar" id="markdown-toc-ajouter-une-barre-de-navigation-navbar">Ajouter une barre de navigation (navbar)</a></li>
      <li><a href="#créer-un-barre-de-navigation-avancée" id="markdown-toc-créer-un-barre-de-navigation-avancée">Créer un barre de navigation avancée</a></li>
      <li><a href="#afficher-les-derniers-articles" id="markdown-toc-afficher-les-derniers-articles">Afficher les derniers articles</a></li>
      <li><a href="#créer-une-nouvelle-page" id="markdown-toc-créer-une-nouvelle-page">Créer une nouvelle Page</a></li>
      <li><a href="#comment-ajouter-un-sommaire--toc--table-of-content" id="markdown-toc-comment-ajouter-un-sommaire--toc--table-of-content">Comment ajouter un sommaire ( TOC : Table of Content)</a></li>
      <li><a href="#comment-ajouter-une-image" id="markdown-toc-comment-ajouter-une-image">Comment ajouter une image</a></li>
      <li><a href="#comment-insérer-un-lien-vers-une-autre-page-de-son-site" id="markdown-toc-comment-insérer-un-lien-vers-une-autre-page-de-son-site">Comment insérer un lien vers une autre page de son site</a></li>
      <li><a href="#comment-insérer-un-bout-de-code-sur-une-ligne" id="markdown-toc-comment-insérer-un-bout-de-code-sur-une-ligne">Comment insérer un bout de code sur une ligne</a></li>
      <li><a href="#personnaliser-le-template-avec-bootstrap" id="markdown-toc-personnaliser-le-template-avec-bootstrap">Personnaliser le template avec Bootstrap</a>        <ul>
          <li><a href="#installer-bootstrap-pour-jekyll" id="markdown-toc-installer-bootstrap-pour-jekyll">Installer Bootstrap pour Jekyll</a></li>
        </ul>
      </li>
      <li><a href="#messages-derreur" id="markdown-toc-messages-derreur">Messages d’erreur:</a>        <ul>
          <li><a href="#the-jekyll-theme-minimal-theme-could-not-be-found" id="markdown-toc-the-jekyll-theme-minimal-theme-could-not-be-found">The jekyll-theme-minimal theme could not be found</a></li>
          <li><a href="#error--could-not-locate-the-included-file-icon-githubhtml" id="markdown-toc-error--could-not-locate-the-included-file-icon-githubhtml">Error:  Could not locate the included file ‘icon-github.html’</a></li>
        </ul>
      </li>
      <li><a href="#liens" id="markdown-toc-liens">Liens</a></li>
    </ul>
  </li>
</ul>

<h2 id="comment-ajouter-une-image">Comment ajouter une image</h2>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>![titre image](http://memofil.github.io/assets/image.png)
</code></pre></div></div>
<h2 id="comment-insérer-un-lien-vers-une-autre-page-de-son-site">Comment insérer un lien vers une autre page de son site</h2>
<p>Exemple d’un lien qui pointe vers cet article :</p>
<div class="language-text highlighter-rouge"><div class="highlight"><pre class="highlight"><code>[--&gt; Mettre en page un site satique]({% post_url 2017-06-04-Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages %})

</code></pre></div></div>
<p>Résultat : <a href="/jekyll/2017/05/22/Mettre-en-page-un-site-statique-avec-jekyll-et-github-pages.html">Mettre en page un site statique</a></p>

<h2 id="comment-insérer-un-bout-de-code-sur-une-ligne">Comment insérer un bout de code sur une ligne</h2>
<p>Pour avoir <code class="highlighter-rouge">index.htlm</code> , il faut entourer le mot par le caractère <strong>`</strong>, tel que :</p>

<div class="language-text highlighter-rouge"><div class="highlight"><pre class="highlight"><code>`index.html`
</code></pre></div></div>

<h2 id="personnaliser-le-template-avec-bootstrap">Personnaliser le template avec Bootstrap</h2>

<h3 id="installer-bootstrap-pour-jekyll">Installer Bootstrap pour Jekyll</h3>
<p>Boostrap fonctionne nativement avec less, pour utiliser Bootstrap avec Jekyll qui utilise Sass, on doit installer <a href="https://github.com/twbs/bootstrap-sass#a-ruby-on-rails" target="_blank">Bootstrap-sass</a> via les gem Ruby :</p>

<ol>
  <li>Install le gem bootstrap-sass :</li>
</ol>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>sudo gem install bootstrap-sass
</code></pre></div></div>

<ol>
  <li>Se rendre à la racine du site jekyll et  ajouter les lignes suivantes au fichier <code class="highlighter-rouge">Gemfile</code>  :
    <div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>gem 'bootstrap-sass', '~&gt; 3.3.7'
gem 'sass-rails', '&gt;= 3.2'
</code></pre></div>    </div>
  </li>
  <li>Afin de réinitialiser la configuration du site jekyll ,  taper :</li>
</ol>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle install
</code></pre></div></div>
<ol>
  <li>
    <p>Créer un répertoire <code class="highlighter-rouge">_sass</code> à la racine du site ou seront stocké les templates .scss de Bootstrap</p>
  </li>
  <li>
    <p>Télécharger le <a href="" target="blank">dépot bootstrap</a> afin d’y récupérer les éléments necessaires à Jekyll pour pouvoir compiler les styles bootstrap. On déplacera alors le dossier <code class="highlighter-rouge">assets/stylesheets/bootstrap</code> et le fichier <code class="highlighter-rouge">assets/stylesheets/_bootstrap.scss</code> dans le dossier <code class="highlighter-rouge">_sass</code> tout juste créé.</p>
  </li>
  <li>
    <p>Modifier le ‘_config.yml’ en y ajoutant les lignes  (<a href="https://jekyllrb.com/docs/assets/#sassscss" target="_blank">docs jekyll</a>):</p>
  </li>
</ol>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>sass:
    sass_dir: _sass
</code></pre></div></div>

<h2 id="messages-derreur">Messages d’erreur:</h2>

<h3 id="the-jekyll-theme-minimal-theme-could-not-be-found">The jekyll-theme-minimal theme could not be found</h3>
<p>En tentant d’exécuter en local Jekyll avec la commande</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle exec jekyll serve
</code></pre></div></div>
<p>On obtient</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>jekyll 3.4.3 | Error:  The jekyll-theme-minimal theme could not be found
</code></pre></div></div>

<p>Le thème est manquant. Il faut ajouter <code class="highlighter-rouge">gem "jekyll-theme-minimal", "~&gt; 0.0.3"</code> au Gemfile et l’installer:</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle install
</code></pre></div></div>

<h3 id="error--could-not-locate-the-included-file-icon-githubhtml">Error:  Could not locate the included file ‘icon-github.html’</h3>

<p>En tentant d’exécuter en local Jekyll avec la commande</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle exec jekyll serve
</code></pre></div></div>
<p>On obtient</p>
<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle exec jekyll serve
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
Configuration file: /home/demiton/git/demiton.github.io/_config.yml
            Source: /home/demiton/git/demiton.github.io
       Destination: /home/demiton/git/demiton.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
     Build Warning: Layout 'post' requested in _posts/2017-06-06-welcome-to-jekyll.markdown does not exist.
  Liquid Exception: Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source. in about.md
jekyll 3.4.3 | Error:  Could not locate the included file 'icon-github.html' in any of ["/home/demiton/git/demiton.github.io/_includes"]. Ensure it exists in one of those directories and, if it is a symlink, does not point outside your site source.

</code></pre></div></div>
<p>Le fichier ‘icon-github.html’ est introuvable, ce dernier est associé au theme minima qui est probablement non installé :</p>

<div class="highlighter-rouge"><div class="highlight"><pre class="highlight"><code>bundle install minima
</code></pre></div></div>

<h2 id="liens">Liens</h2>
<ul>
  <li><a href="http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming" target="_blank">http://literaturegeek.com/2017/02/04/building-research-website-with-jekyll-githubpages-theming</a></li>
  <li><a href="http://veithen.github.io/2015/03/26/jekyll-bootstrap.html" target="_blank">http://veithen.github.io/2015/03/26/jekyll-bootstrap.html</a></li>
  <li><a href="https://simpleit.rocks/how-to-add-bootstrap-4-to-jekyll-the-right-way/" target="blank">https://simpleit.rocks/how-to-add-bootstrap-4-to-jekyll-the-right-way/</a></li>
  <li><a href="https://blog.webjeda.com/jekyll-categories/" target="_blank">https://blog.webjeda.com/jekyll-categories/</a></li>
  <li><a href="http://longqian.me/2017/02/09/github-jekyll-tag/" target="_blank">http://longqian.me/2017/02/09/github-jekyll-tag/</a></li>
  <li><a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/" target="_blank">https://css-tricks.com/snippets/css/a-guide-to-flexbox/</a></li>
  <li><a href="https://www.w3schools.com/css/css3_flexbox.asp" target="_blank">https://www.w3schools.com/css/css3_flexbox.asp</a></li>
</ul>

        </section>

        <footer>
         <section id="downloads" class="clearfix">
          
	  
          <a href="https://github.com/Memofil" id="view-on-github" class="button"><span>View on GitHub</span></a>
	  
        </section>
        
        
          This page was generated by <a href="https://pages.github.com">GitHub Pages</a>.

        </footer>

      </div>
    </div>

    
      <script type="text/javascript">
        (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
        (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
        m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
        })(window,document,'script','//www.google-analytics.com/analytics.js','ga');
        ga('create', 'UA-101155540-1', 'auto');
        ga('send', 'pageview');
      </script>


  </body>
</html>
