function doPost(e){
  
  var estringa = JSON.parse(e.postData.contents);
 
  var payload = start(estringa);
  var data = {
    "method": "post",
    "payload": payload
  }
   
  UrlFetchApp.fetch("https://api.telegram.org/bot5659490958:AAG3YFDJDcNyHimLm6Mo-mnYF-xTiPGZHWY/", data);
}
function start(estringa){
  var id = "1336625931"
  var payload;
   
  if (estringa.message.text){
      payload = {
          "method": "sendMessage",
          "chat_id": id,
          "text": estringa.message.text,
      } 
     
  }
  else if (estringa.message.sticker){
    payload = {
      "method": "sendSticker",
      "chat_id": id,
      "sticker": estringa.message.sticker.file_id
    }
   }
  else if (estringa.message.photo){
    array = estringa.message.photo;
    text = array[1];
    payload = {
      "method": "sendPhoto",
      "chat_id": id,
      "photo": text.file_id
    }
   }
    else {
    payload = {
      "method": "sendMessage",
      "chat_id": id,
      "text": "Try other stuff"
    }
   }
  return payload
}
