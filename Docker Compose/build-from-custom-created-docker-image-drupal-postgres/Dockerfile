# create your custom drupal image here, based of official drupal
# First you need to build a custom Dockerfile in this directory, FROM drupal:9
# Then RUN apt package manager command to install git: apt-get update && apt-get install -y git
# Remember to cleanup after your apt install with rm -rf /var/lib/apt/lists/* and use \ and && properly. You can find examples of them in drupal official image. More on this below under Compose file.
# Then change WORKDIR /var/www/html/themes
# Then use git to clone the theme with: RUN git clone --branch 8.x-4.x --single-branch --depth 1 https://git.drupalcode.org/project/bootstrap.git
# Combine that line with this line, as we need to change permissions on files and don't want to use another image layer to do that (it creates size bloat). This drupal container runs as www-data user but the build actually runs as root, so often we have to do things like chown to change file owners to the proper user: chown -R www-data:www-data bootstrap. Remember the first line needs a \ at end to signify the next line is included in the command, and at start of next line you should have && to signify "if first command succeeds then also run this command"
# Then, just to be safe, change the working directory back to its default (from drupal image) at /var/www/html


FROM drupal:8.8.5

RUN apt-get update && apt-get install -y git \ 
    && rm -rf /var/lib/apt/lists/*  
    # delete cache atleast 10MB

WORKDIR /var/www/html/themes

# specific branch (single branch) latest (depth) copy saves download time & space
RUN git clone --branch 8.x-4.x --single-branch --depth 1 https://git.drupalcode.org/project/bootstrap.git \
    && chown -R www-data:www-data bootstrap
# apache expects user as www-data instead of root which is default user for RUN

WORKDIR /var/www/html



