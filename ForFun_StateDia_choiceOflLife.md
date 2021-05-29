
# Just life
Sometimes we are thinking about our life. What makes us happy, what we want. It is kind of fun creates this as a state diagram.
 - Health?
 - Lot of money? 
 - Wonderful appartment? 
 - Lot of friends? 
 - Love?
 - Be famous artist?
 
There can be things that will undermine a person's path such as illness, break with the love of life, what is your case? Will you fight till the end?

Will you enjoy life to the fullest? Or are you colorblind and all people tell you how colorful the world is?

![possible paths of life](http://www.plantuml.com/plantuml/png/TP7DQkim48NtVeg3L_TUI1xX4fgsD7HJQ3UbTA7OusYAB0dzEFZjgv-OWgbNicRcw9nlVF11k117rVpvznUxtN-qhoHS9p4O1ociPKtUjms01XlD8hkBh7fSIQWWo_ZEyKM6r4elRqghvKdb2nMRqu3s69quAseH9EdiMyO-WelqYVRUG9k02q-4QFTuPDs39d8pZ0riD8A19A5AZEhm8kPSjOud4GYzwO9nnM-PU4e2wcjbkTHEUL-PYMfpnKNAKtCBE0ZbSy8XAwoVEvc3A5k4dC3U93bXcNmj5xu6M04-4raCsONrPIlZOeoLzuz5N_TK0oo3xT6C8mVuo1ttDwGr4qZtuA6v7K2p-VTM-wcK2QCMAk2Qxq5_cHcAXqtxNtPw2ZcLtoDzoEY2npa6l9k8Aok5idAHU1F-4cRzy89rI6SSrJS0)
```plantuml
@startuml
(*) --> "Search for happiness"
   
  "Search for happiness"--> "Build wealth"
   -right-> (*)
  "Search for happiness" --> "Ilnesses"
  If "Curable" then 
   --> [true] "Do not give up. Find every option to heal"
    --> "Pay to private doctors"
     --> "Healed"
    "Healed" --> "Find love"
    -right-> (*)
  else
  --> [false] "find psycho help"
   if "Therapies help" then
     --> [true] "Keep fighting"
     --> "Healed"
     else
     --> [false] "Therapies do not help"
     -->"Commit suicide"
     -right-> (*)
   end if
end if
  
"Search for happiness" --> "Find love"
  if "True love" then
    --> [true] "Enjoy life"
     -right-> (*)
   else
  --> [false] "It ends. It hurts but You will find another love"
   -right-> (*)
  end if
@enduml
```
