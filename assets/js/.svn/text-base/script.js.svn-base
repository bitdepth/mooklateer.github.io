/* Author: Colin Clark

*/



(function(){

	var debug = false,
	scrollT, 
	$el,
	workStart = $('#home').outerHeight(true),
	aboutStart = workStart + $('#work').outerHeight(true),
	contactStart = aboutStart + $('#about').outerHeight(true);

	if(debug){
		frameless('body');
		appendCSS(styles);
	}

	// Append CSS
	function appendCSS(css) {
		if(document.createStyleSheet) {
			document.createStyleSheet(css);
		} 
		else {
			$('<style type="text/css"></style>').html(css).appendTo('head');
		}
	};

	function frameless(target, alignment) {
		Buttons.create(target);
		Grid.create(target);
		Baseline.create(target);
		Resolutions.create(target);
	}


	function updateNav($el){
		$('.nav-main a').removeClass('current');
		$el.addClass('current');
	}

	// Event handlers

	// $('.nav-main a').click(function(){
	// 	$('.nav-main a').removeClass('current');
	// 	$(this).addClass('current');
	// });

	$('.nav-work li a').hover(

		function(){
			$(this).find('.site-info').animate({"bottom": "0"}, {duration: 250, easing: "swing"});
		},

		function(){
			$(this).find('.site-info').animate({"bottom": "-128px"}, {duration: 250, easing: "swing"});
		}
	);

	$("#contact-submit").click(function(){
		$target = $(this);
		$.ajax({
			type: "POST",
			data: {name:$("#contact-name").val(), email:$("#contact-email").val(), message:$("#contact-message").val()},
			url: "email.php",
			dataType: "json",
			beforeSend : function() {
				$target.find('span').text('Sending...');
				$target.find('img').removeClass('hide');
				$target.attr('disabled', true);
				console.log("ok here we go");
			},
			success : function(data) {
				console.log("mission success");
				$target.find('span').text('Message Sent');
				$target.find('img').addClass('hide');

				setInterval(function(){
					$target.find('span').text('Send');
					$target.attr('disabled', false);
				}, 3000)

				//$("#contactform").prepend("<div class='success'>Your message was sent</div>");
			},
			error : function(xhr, status, error) {
				 console.log(xhr);
				 console.log(status);
				 console.log(error);
			}

		});	
		return false;		
	});





	$(window).bind('scrollstop', function(){

		scrollT = $(window).scrollTop();


		if(scrollT >= workStart && scrollT < (aboutStart - 1)){
			$el = $('[href="#work"]');
		} else if (scrollT >= aboutStart && scrollT < (contactStart - 1)){
			$el = $('[href="#about"]');
		} else if (scrollT >= contactStart){
			$el = $('[href="#contact"]');
		} else {
			$el = $('[href="#home"]');
		}

		updateNav($el);

	});

	

    $('a[href^=#]').click(function() {

    	$('#device').css({'height':'200px'});

        if (location.pathname.replace(/^\//, '') == this.pathname.replace(/^\//, '') && location.hostname == this.hostname) {
            var target = $(this.hash);
            target = target.length && target || $('[name=' + this.hash.slice(1) + ']');
            
            if (target.length) {
                var targetOffset = target.offset().top;
                self = this;

                $('html, body').animate(
                	{ scrollTop: targetOffset }, 
                	{ 
                		duration: 'slow',
                		easing: 'easeOutQuad',
                		complete: function(){
		             		window.location.hash = self.hash;
		             		$('#device').css({'height':'0'});
		             	}
                	}
             	);
    
                return false;
            }
        }


    });


	/* Fix for viewport zoom bug on iphone and ipad */

	if (navigator.userAgent.match(/iPhone/i) || navigator.userAgent.match(/iPad/i)) {
	  var viewportmeta = document.querySelector('meta[name="viewport"]');
	  if (viewportmeta) {
	    viewportmeta.content = 'width=device-width, minimum-scale=1.0, maximum-scale=1.0';
	    document.body.addEventListener('gesturestart', function() {
	      viewportmeta.content = 'width=device-width, minimum-scale=0.25, maximum-scale=1.6';
	    }, false);
	  }
	}



}());





	





















