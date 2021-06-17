# Affine_cipher
//implement with java to the Affine cipher with the encryption and decryption

package affine;

import java.util.Scanner;

/**
 *
 * @author Elbostan
 */
public class Affine {
  public static final String ALPHABET = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
 static int n =ALPHABET.length();

   //encyrption message
    public static String encryptionMessage(int a ,String plainText, int b)
    {
        plainText=plainText.toUpperCase();
        
        String CipherText = "";
        
        for (int i = 0; i < plainText.length(); i++)
        {
            int charPosition = ALPHABET.indexOf(plainText.charAt(i));
             int keyVal = ((a*charPosition)+b)%26;
             char replaceVal = ALPHABET.charAt(keyVal);
            CipherText += replaceVal;
    }
  
     return CipherText;        
            
    
    }
    
      static int modInverse(int a, int m) 
    { 
        a = a % m; 
        for (int x = 1; x < m; x++) 
           if ((a * x) % m == 1) 
              return x; 
        return 1; 
    } 
    
    
   public static String decryptionMessage(int a,String cipherText, int b)
    {
        cipherText=cipherText.toUpperCase();
     String plainText="";
     
      for (int i = 0; i < cipherText.length(); i++)
        {
      int charPosition = ALPHABET.indexOf(cipherText.charAt(i));
             int keyVal = (  a *(charPosition-b))%26;
             
               if (keyVal < 0)
            {
                keyVal = ALPHABET.length() + keyVal;
            }
            char replaceVal = ALPHABET.charAt(keyVal);
            plainText += replaceVal;
        }
             
       return plainText;
    }
    public static void main(String[] args) {
        
    
        
        
        
        String Msg="";
        int M ,key;
        int choice;
        int result1,result2;
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the value of M");
        M=sc.nextInt();
        System.out.println("Enter the value of key");
        key=sc.nextInt();
        result1=M;
        result2= n;
        while (result1 != result2) {
        	if(result1 > result2)
                    
                result1 = result1 - result2;
            else
               result2 = result2 - result1;
        }
        int gcd=result2;
     
        if(gcd==1)
        
       {
         System.out.println("Menu:\n1: Encryption\n2: Decryption");
         choice = sc.nextInt();
                 if(choice==1) {
                               System.out.println("Enter the Meaasge to encrpt");
                               Msg=sc.next();
                               System.out.println("Encrypted Message is : " + encryptionMessage(M ,Msg, key) );
                               }
                 else if(choice==2){
                                  System.out.println("Enter the Meaasge to decrpt");
                                  Msg=sc.next();
                               
                                  System.out.println("Decrypted Message is: " +decryptionMessage (modInverse(M, n),Msg,key));
      
                                   }
       }
       }
}
