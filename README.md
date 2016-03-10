# Miguel-Couto-902
<html>
<head>
  <script src='https://cdn.firebase.com/js/client/1.0.17/firebase.js'></script>
  <script src='https://ajax.googleapis.com/ajax/libs/jquery/1.9.0/jquery.min.js'></script>
</head>
<body>
  <div id='mensagens'></div>
  <input type="text" id="nomeusuario" placeholder="Seu nome...">
  <input type="text" id="mensagem" placeholder="Sua mensagem...">
  <script>
    var APP = new Firebase('https://seu-app.firebaseIO.com/');
 
    $('#mensagem').keypress(function (e) {
      if (e.keyCode == 13) {
 
        var msg = $('#mensagem').val();
        var usr = $('#nomeusuario').val();
        APP.push({ nomeusuario: usr, mensagem: msg });
 
        $('#mensagem').val('');
      }
    });
 
    APP.on('child_added', function(snap) {
      var novamensagem = snap.val(); //Nova mensagem recebida.
      carregaMensagem(novamensagem.nomeusuario, novamensagem.mensagem);
    });
 
    function carregaMensagem(nome, mensagem) {
      $('<div/>').text(mensagem)
        .prepend($('<strong/>').text(nome + ': '))
        .appendTo($('#mensagens'));
 
      $('#mensagens')[0].scrollTop = $('#mensagens')[0].scrollHeight;
    };
  </script>
</body>
</html>
