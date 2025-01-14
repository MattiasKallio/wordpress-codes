
# Contact Form 7 - Temporarily Disable Submit Button
This code will disable the submit button for 5 seconds when the form is submitted. This is to prevent multiple submissions of the form. The submit button will be disabled and the text will change to "Sending..." for 5 seconds. After 5 seconds, the submit button will be enabled again and the text will change back to "Send".

Put this in the footer of your page or in a javascript file in the theme or child theme.

   ```javascript
   $('.wpcf7-form').on('submit', function (e) {
      var $form = $(this);
      var $submit = $form.find('input[type="submit"]');

      if (!$submit.hasClass('disabled')) {
         $submit.addClass('disabled');
         $submit.attr('disabled', 'disabled');
         $submit.val('Skickar...');

         setTimeout(function () {
            $submit.removeClass('disabled');
            $submit.removeAttr('disabled');
            $submit.val('Skicka');
         }, 5000);
      }
   });
    ```