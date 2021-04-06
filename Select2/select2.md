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

4. ###### Script Jquery pour un select a choix multiple et possiblité d'ajouter un nouvel element
```
    $(function() {
        $('.select-types').select2({
            tags: true,
            tokenSeparators: [',',' ']
        }).on('change', function(e){
            // on recupère les options selectionnée dans le select (this)
            let label = $(this).find("[data-select2-tag=true]"); 
            //verifie que le label selectionner n'est pas deja dans la base de donnée ou deja inserer
            if(label.length &&  $.inArray(label.val(), $(this).val() != -1)){ 
                //requète ajax pour envoyer les info
                $.ajax({
                    url: "/writer/add/ajax"+label.val(),
                    type: "POST",
                }).done(function(data){
                    //on rajoute la nouvelle option pour ne pas qu'elle ne soit encore considéré comme nouvelle
                    label.replaceWith(`<option selected value="${data.id}">${label.val()}</option>`)
                })
            }
        });

        $('.select-writers').select2({
            tags: true,
            tokenSeparators: [',',' ']
        }).on('change', function(e){
            
        });
    });
```