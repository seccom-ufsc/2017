Site
====

Preparação
----------

Para poder começar a editar o site:

1. Clone o repositório:

   Clonar por HTTPS:
   ```bash
   git clone https://github.com/seccom-ufsc/zeppelin
   ```

   Clonar por SSH:
   ```bash
   git clone git@github.com:seccom-ufsc/zeppelin
   ```

2. Entre no repositório:

   ```bash
   cd zeppelin
   ```

3. Instale as dependências:

   ```bash
   bundle install
   ```

4. Instale um "Listener" de JavaScript, preferencialmente o NodeJS (que vai
   servir de base para várias coisas envolvendo web):

   Arch Linux:
   ```bash
   sudo pacman -S nodejs
   ```

   Ubuntu/Xubuntu/Mint:
   ```bash
   sudo apt install nodejs
   ```

4. Execute o servidor localmente (para testar):

   ```bash
   bundle exec jekyll serve
   ```

5. Abra o site no navegador:
   [127.0.0.1:4000/zeppelin/](127.0.0.1:4000/zeppelin/) (a "/" no final é
   obrigatória).

6. Caso queira que o servidor gere os elementos modificados do site novamente
   após editar algum arquivo, deixe um terminal rodando o servidor com:

   ```bash
   bundle exec jekyll serve -w
   ```

7. Considere, antes de qualquer _deploy_, [reduzir o tamanho do
   site](compression.md).

Throubleshooting
----------------

### Date format not valid

Caso ocorra um erro seguinte erro:

```bash
Error: could not read file /home/jptiz_local/dev/pet/zeppelin/vendor/bundle/ruby/2.4.0/gems/jekyll-3.5.2/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb: Invalid date '<%= Time.now.strftime('%Y-%m-%d %H:%M:%S %z') %>': Document 'vendor/bundle/ruby/2.4.0/gems/jekyll-3.5.2/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb' does not have a valid date in the YAML front matter.
             ERROR: YOUR SITE COULD NOT BE BUILT:
                    ------------------------------------
                    Invalid date '<%= Time.now.strftime('%Y-%m-%d %H:%M:%S %z') %>': Document 'vendor/bundle/ruby/2.4.0/gems/jekyll-3.5.2/lib/site_template/_posts/0000-00-00-welcome-to-jekyll.markdown.erb' does not have a valid date in the YAML front matter.
```

Apenas edite o arquivo `_config.yml`, procurando pela definição
`exclude: [ ... ]` e adicionando `'vendor'` na lista, por exemplo:

```yml
exclude: ['README.md', 'vendor']
```
