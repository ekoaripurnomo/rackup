Local Web Server for AngularJS dan Javascript (Rackup)

* Install Ruby terlebih dahulu, karena web server menggunakan ruby sebagai server nya
* pastikan bundler sudah di install di sebagai ruby managemen aplikasi
* jika belum, install	melalui command line : gem install budler
* buat Gemfile di dalam project, dalam hal ini didalam folder rackup sebagai folder root project
* Gemfile bisa dibuat menggunakan text editor
* isi Gemfile :

	source 'https://rubygems.org'
	gem 'rack'

* isi Gemfile tersebut berarti kita menginstall rack pada bundler
* jalan kan : bundle install <====== difolder project
* akan dihasilkan file Gemfile.lock yang isinya :

	GEM
		remote: https://rubygems.org/
		specs:
			rack (2.0.3)

	PLATFORMS
		x64-mingw32

	DEPENDENCIES
		rack

	BUNDLED WITH
		 1.15.3

* buat file config.ru yang merupakan file configurasi webserver sbb:

			use Rack::Static,
				:urls => ["/images", "/js", "/css", "/templates"],
				:root => "src"

			run lambda { |env|
				[
					200,
					{
						'Content-Type'  => 'text/html',
						'Cache-Control' => 'public, max-age=86400'
					},
					File.open('src/index.html', File::RDONLY)
				]
			}

* keterangan root file aplikasi didalam folder src, folder src sejajar dengan config.ru
	di dalam folder src terdapat folder static seperti /images, /js, /css, /templates, daan folder lain sesuai kebutuhan
	file index.html ada di dalam folder /src

* sesudah file config.ru dibuat, server dapat dijalankan dengan perintah : rackup di terminal command prompt
* Navigate to http://127.0.0.1:9292/ or http://localhost:9292/