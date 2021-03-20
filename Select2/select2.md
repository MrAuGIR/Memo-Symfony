# Mise en oeuvre

1. ###### Télécharger le select2.min.css et le placer dans le dossier public
   
2. ###### Appeler le fichier avec la méthode asset()
`` <link href="{{asset('style/select2.min.css')}}" rel="stylesheet" /> ``

3. ###### Placer le fichier js en bas de page 
   ```
   <script src="https://code.jquery.com/jquery-3.6.0.js" integrity="sha256-H+K7U5CnXl1h5ywQfKtSj8PCmoN9aaq30gDh27Xc0jk=" crossorigin="anonymous"></script>
    <script src="{{asset('script/select2.full.min.js')}}"></script>
    <script>
        
        $(document).ready(function() {
            $('.js-example-basic-single').select2();
        });
    </script>
    ```