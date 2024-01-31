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
//Try catch to catch the error.
try{
    $db= new PDO("mysql:host=localhost;dbname=000904793","root","");
}catch(Exception $e){
    echo"Connection failed";
}
?>