1. cdn de datatable a placer a la fin du fichier
`` https://cdn.datatables.net/v/dt/jq-3.2.1/dt-1.10.16/datatables.min.js ``

3. le cdn css 
   ``<link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.10.23/css/jquery.dataTables.css">``

4. Script en bas de page twig
```
$(document).ready(function(){
    $('#iddelatable').DataTable();
})


```