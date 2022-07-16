<!--index.php-->

<!DOCTYPE html>
<html>
<head>
  	<title>Plagiarism System</title>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
	<!-- Font Awesome -->
	<link  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.1/css/all.min.css" rel="stylesheet" />
	<!-- Google Fonts -->
	<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
	<!-- MDB -->
	<link href="https://cdnjs.cloudflare.com/ajax/libs/mdb-ui-kit/3.10.2/mdb.min.css" rel="stylesheet" />
	<!-- MDB -->
	<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mdb-ui-kit/3.10.2/mdb.min.js"></script>
    
    <link href="https://fonts.googleapis.com/css?family=Poppins:300,400,500,600,700,800,900" rel="stylesheet">
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
	<link rel="stylesheet" href="../include/css/style.css">
</head>
  
<style>
body {font-family: Arial, Helvetica, sans-serif;
      background-image: url("gg.jpg");
      background-size: auto;
    }

form {border: 3px;}

fileToUpload {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

button {
  background-color: #04AA6D;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}

button:hover {
  opacity: 0.8;
}

.cancelbtn {
  width: auto;
  padding: 10px 18px;
  background-color: #f44336;
}


.container {
  padding: 275px 25px;
}


</style>

<body>
<div class="container col-md-4 p-6">
<form action="upload.php" method="post" enctype="multipart/form-data">
    <label for="uname"><b>Select your project:</b></label>
    <input type="file" name="fileToUpload[]" id="fileToUpload" required multiple>
 
    <button type="submit" name="submit" value="Upload Project">Upload</button>
  </div>

  </div>
</div>
</form>
</div>
</body>
</html>





<!--upload.php-->
<?php
if(isset($_POST["submit"])) {
	$total = count((array)($_FILES['fileToUpload']['name']));
	for($i=0; $i<$total; $i++ )
	{
	$file_name = $_FILES['fileToUpload']['name'][$i];
	$file_size =$_FILES['fileToUpload']['size'][$i];
	$file_type=$_FILES['fileToUpload']['type'][$i];
	$file_tmp = $_FILES["fileToUpload"]["tmp_name"][$i];
	if($file_tmp !== false) {
		move_uploaded_file($file_tmp,'C:/xampp/htdocs/plagiarism/'.$file_name);
		if($i==$total-1){
		$path = "C:/xampp/htdocs/plagiarism/sss.py";
		$api = exec($path);
		
		$json_data = json_decode($api,true);
		
?>

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-+0n0xVW2eSR5OomGNYDnhzAbDsOXxcvSN1TPprVMTNDbiYZCxYbOOl7+AMvyTG2x"
      crossorigin="anonymous"
    />
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.3.0/font/bootstrap-icons.css"
    />
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.1.1/mapbox-gl.css"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="style.css" />
    <title>Plagiarism</title>
  </head>
  <body>
  
    <!-- Showcase -->
    <section class="text-light p-5 p-lg-0 pt-lg-5 text-center text-sm-start">
      <div class="container">
        <div class="align-items-center justify-content-between">
          <div>
			<table class="table table-bordered">
			  <thead style="position: sticky;top: 0" class="bg-danger text-light">
				<tr>
				<th colspan="2" class="text-center"> 
				<h1>PLAGIARISM REPORT</h1>
				</th>
				</tr>
				<tr>
				  <th scope="col" width="40%"><h2>File Name</h2></th>
				  <th scope="col" width="60%"><h2>Percentage</h2></th>
				</tr>
			  <thead>
			  <tbody
			  
				<?php
					foreach($json_data as $key => $value){
						$value=$value*100;
				?>
				<tr>
				  <td>
					<?php echo $key;?>
				  </td>
				  <td>
					<div class="progress">
					  <div class="progress-bar <?php if($value>=70){echo 'bg-danger';} else if($value>=40){echo 'bg-warning';} else{ echo 'bg-success';} ?>" role="progressbar" style="width: <?php echo $value; ?>%;" aria-valuenow="<?php echo $value; ?>" aria-valuemin="0" aria-valuemax="100"><?php echo $value; ?>%</div>
					</div>
				  </td>
				</tr>
				<?php }}}}} ?>
			  </tbody>
			</table>
          </div>
        </div>
      </div>
    </section>
	
    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.1/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-gtEjrD/SeCtmISkJkNUaaKMoLD0//ElJ19smozuHV6z3Iehds+3Ulb9Bn9Plx0x4"
      crossorigin="anonymous">
	</script>
  </body>
</html>


<!--ss.py-->


import os
import json


from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

student_files = [doc for doc in os.listdir() if doc.endswith('.txt')]
student_notes = [open(_file, encoding='utf-8').read()
                 for _file in student_files]

def vectorize(Text): return TfidfVectorizer().fit_transform(Text).toarray()
def similarity(doc1, doc2): return cosine_similarity([doc1, doc2])

vectors = vectorize(student_notes)
s_vectors = list(zip(student_files, vectors))

def check_plagiarism():
    plagiarism_results = {}
    global s_vectors
    for student_a, text_vector_a in s_vectors:
        new_vectors = s_vectors.copy()
        current_index = new_vectors.index((student_a, text_vector_a))
        del new_vectors[current_index]
        for student_b, text_vector_b in new_vectors:
            sim_score = similarity(text_vector_a, text_vector_b)[0][1]
            if(sim_score >= 0):
                sim_score = round(sim_score, 1)
                student_pair = sorted((os.path.splitext(student_a)[0], os.path.splitext(student_b)[0]))
                res = (student_pair[0]+' similar to '+ student_pair[1])
                plagiarism_results[res] = sim_score
    api = json.dumps(plagiarism_results)
    return api
      

if __name__ == "__main__":
    print(check_plagiarism())


