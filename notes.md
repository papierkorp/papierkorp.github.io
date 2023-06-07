# Erste Schritte

```bash
jekyll serv #startet den eingebauten Server
```

## Konfiguration

findet über `_config.yml` statt

Default Konfigurationen: https://jekyllrb.com/docs/configuration/default/

## Post Default Layout

http://jekyllrb.com/docs/configuration/front-matter-defaults/

```bash
vi _config.yml
	defaults:
	  -
	    scope:
	      path: "" # ein leerer string an dieser Stelle bezieht alle Projektateien ein
	      type: "posts"
	    values:
	      layout: "default"
```

## Front Matter (Metadaten)

Wird im Post erstellt, und ganz oben mit 3x `-` eingeleitet und beendet.
Wird von Jekyll gelesen und verwendet.

Hier können auch eigene Variablen festgelegt und benannt werden.

Diese Variablen können dann in Templates, Schleifen und IF-Abfragen verwendet werden.

In `_config` können unter `default: values:` default Werte festgelegt werden.

Beispiel:

```yaml
---
layout: post
title:  "Welcome to Jekyll!"
date:   2023-06-06 13:13:20 +0200
categories: jekyll update
---
```

## Eigenes Layout erstellen

```bash
mkdir myblog/_layout
cd _layout
vi default.html page.html post.html

mkdir myblog/_includes
cd _includes
vi header.html footer.html sidebar.html
```

**default.html**
```html
{% include header.html %}
    {{ content }}
{% include footer.html %}
```

### Liquid Templates

https://shopify.github.io/liquid/basics/introduction/

**Bauteile aufrufen**

```html
{% include footer.html %}
```


## Anderes Theme installieren

https://github.com/StartBootstrap/startbootstrap-clean-blog-jekyll


```bash
vi Gemfile #gem "jekyll-theme-clean-blog".
bundle install
vi _config.yml #theme: jekyll-theme-clean-blog
bundle exec jekyll serve
```

https://jekyllthemes.io/theme/alembic

## markdown

als default markdown wird https://kramdown.gettalong.org/quickref.html verwendet.

# Installation

Laut Tutorial: https://jekyllrb.com/docs/step-by-step/01-setup/

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev

#Avoid installing RubyGems packages (called gems) as the root user. Instead, set up a gem installation directory for your user account. The following commands will add environment variables to your ~/.bashrc file to configure the gem installation path:

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

gem install jekyll bundler
```

**Neues Projekt**

```bash
#1 Möglichkeit
jekyll new myblog
cd myblog
bundle exec jekyll serve

#2. Möglichkeit
vi Gemfile #gem "jekyll"
bundle init
```


**Upgrade**

```bash
jekyll -v
gem update jekyll
```


# Publish in Git

https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll

# Eigenes Theme erstellen

- https://medium.com/@jameshamann/creating-your-own-jekyll-theme-gem-1f8180a0e4b8
- https://jekyllrb.com/docs/themes/
- https://www.siteleaf.com/blog/making-your-first-jekyll-theme-part-1/
- https://dev.to/supunkavinda/i-created-a-jekyll-theme-in-375-minutes-eoj
- https://idratherbewriting.com/documentation-theme-jekyll/

Alle templates und Layouts werden in einem Ruby gem gespeichert.

```bash

```

**Publish + Testing**

Bei [Ruby Gems](https://rubygems.org/) regsitrieren um das Theme später hochzuladen.

```bash
jekyll new-theme papierkorp-theme
tree papierkorp-theme
	├── Gemfile 					#verweist auf .gemspec
	├── LICENSE.txt					
	├── README.mkdir				
	├── _data						
	├── _includes					#templates
	├── _layouts					
	│   ├── default.html 			
	│   ├── page.html 				
	│   └── post.html 				
	├── _sass						#css
	├── assets						#static files (main styles.scss)
	└── papierkorp-theme.gemspec	#all ruby gem Daten (Version, Name, Beschreibung...)

jekyll serve  #wird wie eine jekyll site behandelt und kann deshalb gestartet werden
gem build YOURTHEME.gemspec #erstellt eine gem file im Ordner, dieses gem File (Pfad) bei meiner Jekyll Seite hinzufügen

#Zum Finish die gemspec Datei mit Version und so füllen:
vi papierkorp-theme.gemspec

gem push YOURTHEME.gem
gem yank YOURTHEME #theme wieder löschen fals Fehler passiert sind
```