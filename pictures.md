# Galería de imágenes

{% for picture in book.pictures %}
[{{ picture.list_caption }}]({{ picture.backlink }})
{% endfor %}
