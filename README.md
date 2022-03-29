API da Bitcointoyou

Documentação completa: https://apidoc.bitcointoyou.com/

Como criar a signature:

function generateSignature(key, secret, nonce)
{    
    var message = nonce + key;
    var hash = CryptoJS.HmacSHA256(message, secret);
    var hashInBase64 = CryptoJS.enc.Base64.stringify(hash);    
    return hashInBase64;
}
