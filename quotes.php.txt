<?php
/**
 * I Vraj Patel, 000904793, certify that this material is my original work. No other person's work has been used without suitable acknowledgment and I have not made my work available to anyone else.
 * @version 20231206
 * @author Vraj Patel
 * @package COMP 10260 Assignment 4
 */

//Enable error reporting which helps in debugging purpose.
ini_set('display_errors',1);
ini_set('display_startup_errors',1);
error_reporting(E_ALL);

/**
 * This function handles all the main logic for displaying details or providing proper and appropriate details to fornted.
 * It first connects the database then exceute it and then stores in array and then display the array in web page.
 * 
 */
function fetch_Data(){
    //Set pagination parameters
    $pages=10;
    $limit=20;
    $offset=($pages-1)*$limit;

    //Include the file for establishing a database connection
    include "connect.php";
    //SQL query to retrieve quotes with pagination
    $query = "SELECT quotes.quote_text, authors.author_name
    FROM quotes
    JOIN authors ON quotes.author_id = authors.author_id
    LIMIT $limit
    OFFSET $offset 
    ";
    //Prepare the SQL statement 
    $stmt= $db->prepare($query);
    //Execute the SQL statement
    $success=$stmt->execute();
    //Fetch the result as an associative array
    $result= $stmt->fetchAll(PDO::FETCH_ASSOC);
    //Prepare an array to store HTML card elements
    $response= array();
    //Iterate through the result and generate HTML code
    foreach($result as $x){
        $temp='<div class="card mb-3 a4card w-100">'.
        '<div class="card-header" style="Background:#4361ee;">'.$x["author_name"].'</div>'.
        '<div class="card-body d-flex align-items-center" style="Background:#fca311;">'.
             '<p class="card-text w-100">'.$x["quote_text"].'</p>'.
        '</div>'.
        '</div>';
     array_push($response,$temp);
    }
    //Output the JSON encoded array.
    echo json_encode($response);
    
}
//calls the function
fetch_Data();

?>