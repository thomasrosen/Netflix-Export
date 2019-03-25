# Netflix-Export

The best way to download the date, is to use the same api as Netflix. Go into the networks tab in the developers console and look how netflix deoes it.
The URL for ratings should look similar to https://www.netflix.com/api/shakti/v6faf08f4/ratinghistory?pg=0&authURL=1546823913836.0TPYmnE6wCH0k20wfWh4YIQRe+8= (as of 2019/01/07) and the URL for watch history is something like https://www.netflix.com/api/shakti/v6faf08f4/viewingactivity?pg=0&authURL=1546823913836.0TPYmnE6wCH0k20wfWh4YIQRe+8= (as of 2019/01/07)

Another way is to use a script, that parses the HTML page:
## To export ratings (as of 2019/01/07)

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
