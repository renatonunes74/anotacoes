[toc]

# Jekyll no NixOS
- Instale o Jekyll: `nix-env -iAv nixos.jekyll`

## Gerando os arquivos para o Jekyll
- Execute: `jekyll new SITE`
	- SITE -> sera o nome do arquivo construido

## Rodar localmente
- Instalar pacotes Gem no .vendor/cache: `nix-shell -p bundler --run "bundle install --gemfile=Gemfile --path vendor/cache && bundle exec jekyll serve"`
	- isso evitara problemas de não encontrar o `path` do Nix

### Testado
#### Temas
- [Just The Docs](https://just-the-docs.com/)

# Links auxiliares
- [Documentação oficial](https://jekyllrb.com/docs/)
