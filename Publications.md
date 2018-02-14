# Publications
  * Publication list from [inspires-HEP](http://inspirehep.net/search?ln=en&p=author%3A%22{{site.username_spires}}%22+AND+collection%3Aciteable&rg=300&jrec=1)
    * [Collection of Journal publication](http://inspirehep.net/search?p=exactauthor%3A{{site.username_spires}}+collection%3APublished)
  * Profile from [inspires-HEP](http://inspirehep.net/author/profile/J.Goh.1)

<a data-toggle="collapse" href="#inspire-code">Bash script to list up papers</a>
<div id="inspire-code" class="collapse">
<pre>
#/bin/bash

MAXITEM=700
NPERPAGE=200
SPIRESID={{site.username_spires}}
for i in `seq 1 $NPERPAGE $MAXITEM`; do
    echo wget 'http://inspirehep.net/search?ln=en&p=author%3A%22${SPIRESID}%22+AND+collection%3Aciteable&rg=${NPERPAGE}&jrec=1' -O p${i}.html
done
for i in `cat p*.html | grep -o '<a class="authorlink" href="/record/[0-9]\+"><i> et al.</i></a>' | grep -o '[0-9]\+'`; do
    wget "http://inspirehep.net/record/$i" --quiet -O a.html; cat a.html | \
        grep '^<meta' | awk -F\" '{if($4 == "citation_title" || $4 == "citation_doi" || $4 == "citation_publication_date")print $2}';
    echo -n "number of authors : "; grep 'Show all [0-9]\+ authors' a.html | \
        awk '{print $5}'
done > count.txt
</pre>

_Beta_: publication per year
![histogram](http://inspirehep.net/img/tmp/8/8e68d2e3ef68853fa356afd65a365b2a.png)
