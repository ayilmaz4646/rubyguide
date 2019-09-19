## Metotlar
### Methot Tanımları

* Metotun beklediği parametre(ler) varsa, `def` ile parantez kullanın. Eğer metot bir parametre beklemiyorsa, parantez kullanmanız gerekmez.

	```ruby
	def some_method
	  #metod içeriği
	end
	
	def some_method_with_parameters(arg1, arg2, ...)
	  #metod içeriği
	end

	```
* Metot parametrelerini tek tek tanımlamak yerine hash içerisinde göndererek metot içerisinde tanımlamak daha kullanışlıdır.

	```ruby
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

	```ruby
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

	```ruby
	# kötü
	@current_user = User.find 2312
	
	# iyi
	@current_user = User.find(2312)

	```
* Metotun ilk parametresi parantez içerisindeyse;

	```ruby
	# kötü
	put! (x + y) % len, value
	
	# iyi
	put!((x + y) % len, value)
	```
* Metot adı ile parantez arasına asla boşluk bırakmayın.

	```ruby
	# kötü
	f (3 + 2) + 1
	
	# iyi
	f(3 + 2) + 1
	```
* Metot deger beklemiyorsa, parantez kullanmanız gerekmez.

	```ruby
	# kötü
	nil?()
	
	# iyi
	nil?
	```
* Metot bir değer döndürmezse(veya önemsenmezse), parentez kullanımı isteğe baağlıdır. Eğer parametreler çoksa, parantez kodun okunabilirliğini kolaylaştırır.

	```ruby
	# iyi
	render(:partial => 'foo')

	# iyi
	render :partial => 'foo'
	```

* Eğer metot son değişken olarak hash bekliyorsa, `{` `}` parantez kullanmayın.

	```ruby
	# kötü
	get '/v1/reservations', { :id => 46352 }
	
	# iyi
	get '/v1/reservations', :id => 46352
	
	```

### Koşullar

* Eğer ` if/unless `metotunuz birden fazla satırdan oluşuyorsa (multi-line), Asla `then` kullanmayınız.

	```ruby
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
* Metot içeriği ve koşulları basit ise tek satır kullanım iyidir.

	```ruby
	# kötü
	add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[: trebuchet_experiments_on_page].empty?
	
	# güzel
	if request_opts[:trebuchet_experiments_on_page] &&
	  !request__opts[:trebuchet_experiments_on_page].empty?
	  
	  add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
	end
	
	# kötü - Karmaşık. Birden çok satır ve yorum gerektiriyor :(
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
* Eğer `unless` yerine `if` operatörünü kullanabiliyorsanız, `if` i tercih ediniz.

	```ruby
	# kötü
	unless x == 10
	  ...
	end
	
	# iyi
	if x != 10
	  ...
	end
	
	# kötü
	unless x < 10
	  ...
	end
	
	# iyi
	if x >= 10
	  ...
	end
	
	# güzel
	unless x === 10
	  ...
	end
	```
* `if/unless/while` koşullarında, parantezden kaçının.

	```ruby
	# kötü
	if (x > 10)
	  ...
	end
	
	# iyi
	if x > 10
	  ...
	end
	```

### Ternary Operatörü

Kısaltılmış if yapısı da diyebiliriz( `if` kullanılmadan :) ).

  örn:
  ``` 
    not > 50 ? durum = 'geçtin' : durum = 'kaldın'
  ```
  
* Koşullar, kapsamlı ise ternary operatöründen`(?:)` kaçının. Tek Satırlık koşullarda, ternary operatörü tercih edin.

	```ruby
	# kötü
	result = if some_condition then something else something_else end
	
	# iyi
	result = some_condition ? something : something_else
	```
* İç içe geçmiç ternary operatör kullanmak yerine, `if/else` yapsını tercih edin.

	```ruby
	# kötü
	some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else
	
	# iyi
	if some_condition
	  nested_condition ? nested_something : nested_something_else
	else
	  something_else
	end
	```
* ternary operatörlerde çoklu koşullardan kaçının.
* Çok satırlı(multi-line) ternary operatör `(?:)` yerine, `if/then/else/end` i tercih edin.

	```ruby
	# kötü
	some_really_long_condition_that_might_make_you_want_to_split_lines ? 
		something : something_else
	
	# iyi
	if some_really_long_condition_that_might_make_you_want_to_split_lines
	  something
	else
	  something_else
	end
	```
	
### İç içe Koşullar
* İç içe kullanımı önlemek ([daha fazla bilgi için](http://blog.timoxley.com/post/47041269194/avoid-else-return-early))
	
	Genel ilkeleri özetlersek:
	* Fonksiyonun artık birşey yapamadığını gördüğünüz zaman hemen geri dönün.
	* İç içe girintiyi farkettiğiniz durumda, bu durumu gidermeye çalışın. Böyle yaparak kodunuzun, okunabilirlik ve anlaşılabilirliğini arttırmış olursunuz.
	* Önemli akışlar, az girinti gerektirir.
	
	```ruby
	# kötü
	def compute
	  server = find_server
	  if server
	    client = server.client
	    if client
	      request = client.make_request
	      if request
	        process_request(request)
	      end
	    end
	  end
	end
	
	# iyi
	def compute
	  server = find_server
	  return unless server
	  client = server.client
	  return unless client
	  request = client.make_request
	  return unless request
	  process_request(request)
	end
	```
	Döngü içlerinde, iç içe yapılar yerine `next` i tercih edin.
	
	```ruby
	# kötü
	[0, 1, 2, 3].each do |item|
	  if item > 1
	    puts item
	  end
	end
	
	# iyi
	[0, 1, 2, 3].each do |item|
	  next unless item > 1
	  puts item
	end
	```
