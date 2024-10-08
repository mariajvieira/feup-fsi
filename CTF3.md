Week 3

Wordpress version: 5.8.1

Plugins instalados e versões dos mesmos:
Para encontrar os plugins instalados inspecionámos o código fonte do site.
- Woocommerce 5.7.1 (src="http://143.47.40.175:5001/wp-content/plugins/woocommerce/assets/js/frontend/woocommerce.min.js?ver=5.7.1")
- Mstore-api 1.0.0 (src="http://143.47.40.175:5001/wp-content/plugins/mstore-api/assets/js/mstore-inspireui.js?ver=1.0.0")

Possíveis utilizadores e nomes de utilizadores:
- Para descobrir o utilizador com id=1, adicionámos "/?author=1" ao URL do site, onde descobrimos que este utilizador era o "admin".
- Ao testar "/?author=2", o site foi redirecionado para a "shop". Com isto concluímos que o id 2, embora exista, pode estar vinculado a um utilizador com outra função, provavelmente relacionado ao WooCommerce.
- Não foram encontrados mais utilizadores com os restantes ids que testamos.

Pesquisa por vulnerabilidades: