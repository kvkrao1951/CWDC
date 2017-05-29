<?php

	$result = "";

	if (isset($_POST["city"])) {

		$for_city = "http://www.weather-forecast.com/locations/".$_POST['city']."/forecasts/latest";

		$str_to_search = "3 Day Weather Forecast Summary:";
		
		if ($forecast = @file_get_contents($for_city)) {

			$start_pos = strpos($forecast,$str_to_search)+strlen($str_to_search);

			$end_pos = strpos($forecast,"</p>", $start_pos);

			$summary = substr($forecast, $start_pos, $end_pos - $start_pos);

			$result = "<div class='alert alert-success'><h5>Forecast for ".strtoupper($_POST['city'])." for next 3 Days..</h5>"."<p>".strip_tags($summary)."</p></div>";


		} else {

			$result = "<div class='alert alert-danger'><p>Error in the city name entered or I don't have that city in my database. Try another city</p></div>";

		}

	}

?>

<!DOCTYPE html>

<html lang="en">
	
	<head>
	  
		<!-- Required meta tags -->
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

		<!-- Bootstrap CSS -->
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/css/bootstrap.min.css" integrity="sha384-rwoIResjU2yc3z8GV/NPeZWAv56rSmLldC3R/AZzGRnGxQQKnKkoFVhFQhNUwEyJ" crossorigin="anonymous">

		<title>Weather Scraper</title>
		
		<style type="text/css">
		
			#main_body {
				
				background-image: url(background_01.png);
				
				background-size: 100% 100%;
				
				background-repeat: no-repeat;
				
				height: 100vh;
				
				text-align: center;
				
				padding: 50px;
				
			}
			
			#city {
				
				width: 350px;
				
				margin: 50px auto 20px auto;
				
			}
			
			#form_btn {
				
				margin: 10px auto 50px auto;
			}
			
			#show_forecast {
				
				margin 100px auto 20px auto;
				
				width: 350px;
			}
			
		</style>
	  
	</head>
	
	<body>
	  
			<div class="jumbotron" id="main_body">
				
		  		<h1 class="display-4"><strong>What's the Weather?</strong></h1>
				
				<h4>Enter the name of a city.</h4>
				
				<div class="container">
							
					<form method="post">

						<div class="form-group">

							<input 
								   type="text" 
								   class="form-control" 
								   id="city" 
								   name="city" 
								   value="<?php if (isset($_POST['city'])) { echo htmlentities($_POST['city']); } ?>"
							>

						</div>

						 <button type="submit" class="btn btn-primary" id="form_btn">Submit</button>
								
					</form>
							
				</div>
				
				<div class="container" id="show_forecast">
				
					<?php
					
						echo $result;
					
					?>
					
				</div>

			</div>

			<!-- jQuery first, then Tether, then Bootstrap JS. -->

			<script src="https://code.jquery.com/jquery-3.1.1.slim.min.js" integrity="sha384-A7FZj7v+d/sdmMqp/nOQwliLvUsJfDHW+k9Omg/a/EheAdgtzNs3hpfag6Ed950n" crossorigin="anonymous"></script>

			<script src="https://cdnjs.cloudflare.com/ajax/libs/tether/1.4.0/js/tether.min.js" integrity="sha384-DztdAPBWPRXSA/3eYEEUWrWCy7G5KFbe8fFjk5JAIxUYHKkDx6Qin1DkWx51bBrb" crossorigin="anonymous"></script>

			<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-alpha.6/js/bootstrap.min.js" integrity="sha384-vBWWzlZJ8ea9aCX4pEW3rVHjgjt7zpkNpZk+02D9phzyeVkE+jo0ieGizqPLForn" crossorigin="anonymous"></script>
	  
	</body>
	
</html>
