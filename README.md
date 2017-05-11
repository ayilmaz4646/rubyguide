## Metotlar
### Methot Tanımları
* Metotun beklediği parametre(ler) varsa, `def` ile parantez kullanın. Eğer metot bir parametre beklemiyorsa, parantez kullanmanız gerekmez.

	```
	def some_method
	  #metod içeriği
	end
	
	def some_method_with_parameters(arg1, arg2, ...)
	  #metod içeriği
	end

	```
* Metot parametrelerini tek tek tanımlamak yerine hash içerisinde göndererek metot içerisinde tanımlamak daha kullanışlıdır.

	```
	# kötü
	def obliterate(things, gently = true, except = [], at = Time.now)
		....
	end
	
	# iyi
	def obliterate(things, options = {})
		options = {
			gently: true, #burada kullanılan parametreler için
			except = [],  #acıklama yazmak, ileride bu metotu kullananlar için
			at: Time.now, #sağlıklı bir yöntem olabilir.
		}.merge(options)
		....
	end

	```
* Tek satırlık methot yazımlarından kaçının.

	```
		# kötü
		def too_much; something; something_else; end
		
		# iyi
		def some_method
			...
		end
	```
### Metot Çağrıları
metot çağrılarında **parantez kullanın**:
* Eğer metot bir değer döndürüyorsa

	```
	# kötü
	@current_user = User.find 2312
	
	# iyi
	@current_user = User.find(2312)

	```
* Metotun ilk parametresi parantez içerisindeyse;

	```
	# kötü
	put! (x + y) % len, value
	
	# iyi
	put!((x + y) % len, value)
	```
* Metot adı ile parantez arasına asla boşluk bırakmayın.

	```
	# kötü
	f (3 + 2) + 1
	
	# iyi
	f(3 + 2) + 1
	```
* Metot deger beklemiyorsa, parantez kullanmanız gerekmez.

	```
	# kötü
	nil?()
	
	# iyi
	nil?
	```
* Metot bir değer döndürmezse(veya önemsenmezse), parentez kullanımı isteğe baağlıdır. Eğer parametreler çoksa, parantez kodun okunabilirliğini kolaylaştırır.

	```
	# iyi
	render(:partial => 'foo')

	# iyi
	render :partial => 'foo'
	```

* Eğer metot son değişken olarak hash bekliyorsa, `{` `}` parantez kullanmayın.

	```
	# kötü
	get '/v1/reservations', { :id => 46352 }
	
	# iyi
	get '/v1/reservations', :id => 46352
	
	```