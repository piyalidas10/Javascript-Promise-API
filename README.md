Javascript Promise to fetch Api Data

    let myPromise = new Promise(function(resolve, reject){
      //asynchronous code goes here
    });
    
The executor is called automatically and immediately (by the new Promise).
The executor receives two arguments: resolve and reject — these functions are pre-defined by the JavaScript engine. So we don’t need to create them. Instead, we should write the executor to call them when ready.
The then() method returns a Promise. The XMLHttpRequest method send() sends the request to the server. If the request is asynchronous (which is the default), this method returns as soon as the request is sent and the result is delivered using events. If the request is synchronous, this method doesn't return until the response has arrived.

It takes up to two arguments: callback functions for the success and failure cases of the Promise.

    let myPromise = new Promise(function(resolve, reject){
      let xhttp = new XMLHttpRequest();
      xhttp.open("GET", "http://piyalidas.in/webservice/webservice.php?type=all&format=json");

        xhttp.onload = () => {  // () => means function(). onload not worked in safari, onreadystatechange works
          if (xhttp.status === 200) {
            resolve(xhttp.response); // we got data here, so resolve the Promise
          } 
          else {
            reject(Error("Error fetching data.")); // status is not 200 OK, so reject
          }
         };		

        xhttp.send(); //Sends the request to the server (used for GET)
    });

    myPromise.then(
      data => {
      this.projects = JSON.parse(data);
      console.log(this.projects.posts);
      document.writeln("<p>Project ID : "+this.projects.posts[0].post.project_id+"</p>");
      document.writeln("<p>Project Name : "+this.projects.posts[0].post.project_name+"</p>");
      document.writeln("<p>Project Type : "+this.projects.posts[0].post.project_type+"</p>");
      document.writeln("<p>Project Language : "+this.projects.posts[0].post.LanguageName+"</p>");
      },
      error => {
        document.writeln("<h1>Promise rejected.</h1>");
        document.writeln("<h1>"+error.message+"</h1>");
      }
    );
    
    
The resulting promise object has internal properties:

state — initially “pending”, then changes to either “fulfilled” or “rejected”,
result — an arbitrary value of your choosing, initially undefined.
When the executor finishes the job, it should call one of the functions that it gets as arguments:

resolve(value) — to indicate that the job finished successfully:
sets state to "fulfilled",
sets result to value.
reject(error) — to indicate that an error occurred:
sets state to "rejected",
sets result to error.


