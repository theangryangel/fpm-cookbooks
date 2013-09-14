# fpm-cookbooks
A collection of [fpm](https://github.com/jordansissel/fpm) cookbooks. For when
you want shit quickly, and don't care about the politics.

## Local apt repository
  - ```mkdir -p /var/local/apt```
  - Copy debs into /var/local/apt
  - ```dpkg-scanpackages /var/local/apt /dev/null | gzip -9c > /var/local/apt/Packages.gz```
  - Add local apt source ```deb file:/var/local/apt ./```
  - ```apt-get update```
  - Don't forget to dpkg-scanpackages when you add new debs
