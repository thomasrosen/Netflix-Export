# Netflix-Export

## To export ratings (2019/01/07)

	var results=[];
	var els = document.querySelectorAll('.retableRow');
	for (let el of els){
		let result = {};
	
		if(el.querySelector('.thumbs-component').classList.contains('rated-up')){
			result.rating = "up";
		}else if(el.querySelector('.thumbs-component').classList.contains('rated-down')){
			result.rating = "down";
		}

		result.date = el.querySelector('.date').innerText;
		result.title = el.querySelector('.title').innerText;
		result.netflix_link = el.querySelector('.title a').getAttribute('href');
	
		results.push(result);
	}
	console.log(JSON.stringify({ratings:results}));
