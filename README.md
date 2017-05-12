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
###Koşullar
* Eğer ` if/unless `metotunuz birden fazla satırdan oluşuyorsa (multi-line), Asla `then` kullanmayınız.

	```
	 # kötü
	 if some_condition then
	   ...
	 end
	 
	 # iyi
	 if some_condition
	   ...
	 end
	 ```
* Eğer `while` veya `until` metotunuz, multi-line ise Asla `do` kullanmayınız.

	```ruby
	 # kötü
	  while x > 5 do
	  	...
	  end
	  
	  until x > 5 do
	  	...
	  end

	 # iyi
	 while x > 5
	  ...
	 end

	 until x > 5
	  ...
	 end
	 
	```
* `and`, `or`, `not` yerine `&&`, `||`, `!` kullanınız.
* Metot içeriği ve koşulları basit ise tek satır kullanım iyidir. Aksi takdirde 'tek satır' da yazacağım diye de b*kunu çıkarmayın.

	```ruby
	 #kötü 
 add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[:trebuchet_experiments_on_page].empty?
 
 	# güzel
 	if request_opts[:trebuchet_experiments_on_page] &&
       !request_opts[:trebuchet_experiments_on_page].empty?
      
      add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
end
	
	# kötü - Karmaşıktır, birden çok satır ve yorum gerektiriyor :(
	parts[i] = part.to_i(INTEGER_BASE) if !part.nil? && [0, 2, 3].include?(i)
	
	# güzel
	return if reconciled?

	```
* Asla `unless` ile `else` i kullanmayınız. Olumlu durumuyla tekrardan yazın.

	```ruby
	# kötü
	unless success?
	  puts 'failure'
	else
	  puts 'success'
	end
	
	# iyi
	if success?
	  puts 'success'
	else
	  puts 'failure'
	end
	
	```
* `unless` metotunda, birden fazla koşul kullanmaktan kaçının.

	```ruby
	# kötü
	unless foo? && bar?
	   ...
	end
	
	# iyi
	if !(foo? && bar?)
	  ...
	end
	```
