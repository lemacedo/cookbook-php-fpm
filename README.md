Description
===========

Installs and configures PHP-FPM (FastCGI Process Manager), an alternative PHP FastCGI implementation with some additional features useful for sites of any size, especially busier sites.  It's like the `unicorn` of the PHP world dawg.

Requirements
============

Platform
--------

* Debian, Ubuntu
* CentOS, Red Hat, Fedora
* Amazon Linux

Cookbooks
---------

* apt (leverages apt_repository LWRP)
* yum (leverages yum_repository LWRP)

The `apt_repository` and `yum_repository` LWRPs are used from these cookbooks to create the proper repository entries so the php-fpm package downloaded and installed.

Description
==========

Creates a PHP-FPM configuration file at the path specified.  Meant to be deployed with a service init scheme/supervisor such as runit.  Please see the `application::php-fpm` recipe for a complete working example. In depth information about PHP-FPM's configuration values can be [found in the PHP-FPM documentation](http://php.net/manual/en/install.fpm.configuration.php).

Usage
=====
Simply include the recipe where you want PHP-FPM installed. Default pool __www__ will be created. To disable pool creation set default['php-fpm']['pools'] to false.

To customize settings and pools you can override default attributes.

### Usage in roles:
```ruby
name "php-fpm"
description "php fpm role"
run_list "recipe[php-fpm]"
override_attributes "php-fpm" => {
	"pools" => {
		"default" => {
			:enable => true
		},
		"www" => {
			:enable => "true",
			:cookbook => "another-cookbook",
			:process_manager => "dynamic",
			:max_requests => 5000,
			:php_options => { 'php_admin_flag[log_errors]' => 'on', 'php_admin_value[memory_limit]' => '32M' }
		}
	}
}
```

Creating pools in recipes
=========================
### Create PHP-FPM pool named 'www' with default settings:
```ruby
php_fpm_pool "www"
```

### Create PHP-FPM pool named 'www' with custom settings:
```ruby
php_fpm_pool "www" do
  cookbook "another-cookbook" # get template from another cookbook
  process_manager "dynamic"
  max_requests 5000
  php_options 'php_admin_flag[log_errors]' => 'on', 'php_admin_value[memory_limit]' => '32M'
end
```

### Delete PHP-FPM pool named 'www':
```ruby
php_fpm_pool "www" do
  enable false
end
```

License and Author
==================

Author:: Seth Chisamore (<schisamo@opscode.com>)

Copyright:: 2011, Opscode, Inc

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Tradução para o Português-Br

Descrição
===========

Instala e configura o PHP- FPM ( FastCGI Process Manager ) , uma implementação alternativa FastCGI PHP com alguns recursos adicionais úteis para sites de qualquer tamanho , locais especialmente mais movimentadas. É como o ` unicorn` do dawg mundo PHP.

Requisitos
============

Plataforma
--------

* Debian, Ubuntu
* CentOS, Red Hat, Fedora
* Amazon Linux

Cookbooks
---------
* apt (leverages apt_repository LWRP)
* yum (leverages yum_repository LWRP)

O ` ` apt_repository` e LWRPs yum_repository` são usados ​​a partir desses livros de receitas para criar as entradas de repositório adequadas para que o pacote php- fpm baixado e instalado .

Descrição
==========

Cria um arquivo de configuração do PHP- FPM no caminho especificado . Concebido para ser implantado com um esquema de inicialização serviço / supervisor como runit . Por favor, veja a aplicação :: receita ` php- fpm` para um exemplo de trabalho completo . Informações detalhadas sobre os valores de configuração do PHP- FPM pode ser [Procure a pasta PHP-FPM na documentação](http://php.net/manual/en/install.fpm.configuration.php).

Uso
=====
Basta incluir a receita onde você quer PHP- FPM instalado. Pool padrão __www__ será criado. Para desativar pool Conjunto criação padrão['php-fpm']['pools'] para verdadeiro.

Para personalizar as configurações e piscinas você pode substituir atributos padrão .

### Usando de linhas:
```ruby
name "php-fpm"
description "php fpm role"
run_list "recipe[php-fpm]"
override_attributes "php-fpm" => {
	"pools" => {
		"default" => {
			:enable => true
		},
		"www" => {
			:enable => "true",
			:cookbook => "another-cookbook",
			:process_manager => "dynamic",
			:max_requests => 5000,
			:php_options => { 'php_admin_flag[log_errors]' => 'on', 'php_admin_value[memory_limit]' => '32M' }
		}
	}
}
```

Creating pools in recipes
=========================
### Crie PHP-FPM pool named 'www' com valores padrões:
```ruby
php_fpm_pool "www"
```

### Crie PHP-FPM renomeando 'www' com a personalização dos comandos:
```ruby
php_fpm_pool "www" do
  cookbook "another-cookbook" # get template from another cookbook
  process_manager "dynamic"
  max_requests 5000
  php_options 'php_admin_flag[log_errors]' => 'on', 'php_admin_value[memory_limit]' => '32M'
end
```

### Delete PHP-FPM e nome 'www':
```ruby
php_fpm_pool "www" do
  enable false
end
```

licença e Autor
==================
Author:: Seth Chisamore (<schisamo@opscode.com>)

Copyright:: 2011, Opscode, Inc

Licenciado sob a Licença Apache, Versão 2.0 ( a "Licença" );
você não pode usar esse arquivo exceto em conformidade com a Licença .
Você pode obter uma cópia da Licença em

    http://www.apache.org/licenses/LICENSE-2.0

A menos que exigido por lei aplicável ou acordado por escrito, o software
distribuído sob a Licença é distribuído " COMO ESTÁ" ,
SEM GARANTIAS OU CONDIÇÕES DE QUALQUER TIPO, expressa ou implícita .
Consulte a licença para as permissões específicas ao seu idioma e
limitações sob a Licença .