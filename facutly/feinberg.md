---
layout: default
title: Evan Feinberg
permalink: /feinberg/
---

<!-- Page content -->
<!-- Insert Profiles data here -->

<!-- Grid -->
  <div class="w3-light-grey w3-padding-64" id="about">


    <!-- Blog entry -->
    <div class="w3-card-4 w3-margin w3-white">
  	<div id="profiles_photo_container"></div>
      <div class="w3-container w3-padding-8">
        <h4 id="profiles_name"></h4>
        <p id="profiles_narrative"></p>

<!-- add lab website link-->


<h2>Lab Website</h2>
  <ul>
      <li id=""><a href="http://www.evanfeinberglab.com/">Feinberg Lab Website</a></li>
  </ul>

        <h2>Connect</h2>
    	  <ul>
    	    <li id="profiles_email_link_container"></li>
    	    <li id="profiles_page_link_container"></li>
    	  </ul>

    	  <div id="profiles_awards"><h2>Awards</h2></div>
    	  <div id="profiles_publications"><h2>Publications</h2></div>

      </div>
    </div>

<!-- load a recent version of jQuery -->
<script type="text/javascript" src="//ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>

<!-- get data from the UCSF Profiles API -->
      <script>

      // we're grabbing data from the UCSF Profiles JSON API v2
      // details at http://opendata.profiles.ucsf.edu/json-v2.html

      // we get the Profiles URL name from the URL, e.g. "http://profiles.ucsf.edu/jeanette.brown"
      // but you can also specify people by FNO, Profiles ID, Employee ID, etc.
        add_profiles_user_content('ProfilesURLName', 'evan.feinberg');
      // for example try commenting out the line above, and uncommenting the line below
      // add_profiles_user_content('FNO', 'Jeffrey.Bluestone@ucsf.edu');

      function add_profiles_user_content (identifier_type, identifier) {
          $.getJSON('http://api.profiles.ucsf.edu/json/v2/?source=JSON_API_v2_example_script_change_this_in_your_own_app&' + identifier_type + '=' + identifier + '&callback=?',
      	      function(response) {
      		  if (response) {
      		      if (response.error) { // if UCSF Profiles reports an error, can do something with that here
      			  if (window.console && window.console.log) {
      			      console.log('Error from UCSF Profiles API: ' + response.error);
      			      // alert('Error from UCSF Profiles API: ' + response.error);
      			  }
      		      } else {

      			  $(document).ready(function() {   // execute the following code after DOM is ready

      			      var data = response.Profiles[0];

      			      if (data.Name) { // show name, if we have it
      				  $('#profiles_name').text(data.Name);
      			      }
      			      if (data.ProfilesURL) { // add link to Profiles
      				  $('#profiles_page_link_container').empty().show().append('<a href="' + data.ProfilesURL + '" title="Go to UCSF Profiles, powered by CTSI" rel="me">UCSF Profiles page</a>');
      			      } else {
      				  $('#profiles_page_link_container').empty().hide();
      			      }
      			      if (data.PhotoURL) { // show photo, if we have it
      				  $('#profiles_photo_container').empty().show().append($('<img class="img-circle" id="profiles_photo" />').attr('src', data.PhotoURL).error(function(){this.style.display='none'}));
      			      } else {
      				  $('#profiles_photo_container').empty().hide();
      			      }
      			      if (data.Narrative) { // show narrative, if we have it
      				  // truncate text to 500 characters, and delete any partial last sentence
      			          var truncated_narrative = data.Narrative.substr(0,500).replace(/[\s\r\n]/g, " ").replace(/^(.+\.[\s\n\r]).*?$/g, "$1");
      				  $('#profiles_narrative').show().text(truncated_narrative);
      			      } else {
      				  $('#profiles_narrative').hide();
      			      }
      			      if (data.Email) { // show narrative, if we have it
      				  $('#profiles_email_link_container').empty().show().append('<a href="mailto:' + data.Email + '">' + data.Email + '</a>');
      			      } else {
      				  $('#profiles_email_link_container').hide();
      			      }
      			      if (data.Publications && data.Publications.length > 0) {
      				  $('#profiles_publications ol').remove();
      				  $('#profiles_publications').show().append($('<ol id="profiles_publications_list"></ol>'));
      				  jQuery.each(data.Publications, function() {
      				      var li = $('<li id="profiles_publications_li" />'); // create new list item
      				      li.append(this.PublicationTitle + ' '); // add the publication name
      				      if (this.PublicationSource && this.PublicationSource.length > 0) { // ...and a link, if available
      					  li.append($('<a class="profiles_publication_link" />').attr('href', this.PublicationSource[0].PublicationSourceURL).text('View on ' + this.PublicationSource[0].PublicationSourceName));
      				      }
      				      $('#profiles_publications_list').append(li); // insert the list item
      				  });
      			      } else {
      				  $('#profiles_publications').hide();
      			      }
      			      if (data.AwardOrHonors && data.AwardOrHonors.length > 0) {
      				  $('#profiles_awards_list').remove();
      				  $('#profiles_awards').show().append($('<ul id="profiles_awards_list"></ul>'));
      				  jQuery.each(data.AwardOrHonors, function() {
      				      var li = $('<li />').append(this.Summary);
      				      $('#profiles_awards_list').append(li);
      				  });
      			      } else {
      				  $('#profiles_awards').hide();
      			      }

      			      $("html, body").animate({ scrollTop: 0 }, 100);
      			      $("[id^='profiles_']:visible").fadeIn(100).fadeOut(100).fadeIn(100);
      			  });

      		      }
      		  }
      	      }
      	     );
      }

      function highlight_profiles_content (seconds) {
          var ms = (seconds || 1) * 1000;
          $( "[id^='profiles_']" ).addClass('highlighted');
          setTimeout(function() {
      	$( "[id^='profiles_']" ).removeClass('highlighted');
          }, ms);
      }
      </script>


</div>
<!-- End page content -->
