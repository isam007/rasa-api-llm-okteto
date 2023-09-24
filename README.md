# LLM Chatbot Deployment to Okteto.net
1. Login to your account in Okteto.net using github account (note generic emails are not accepted - has to be business email)
2. Add a namespace (mine here is ibot-isam007, so make sure to replace it with your namespace)
3. Open new terminal window in VS code and make sure you are still in rasa virtual environment. 
   ! If you are lost about this point, check dev instructions to my https://github.com/isam007/rasabot-okteto repo
4. Replace all endpoints using ibot-isam007 namespace in this project with your own namespace (use find-replace)
5. If you made any changes to dataset, make sure to train your model(`rasa train`)
6. Run following commands in terminal one by one (don't forget to use your own namespace instead of ibot-isam007):
   -- `okteto namespace use ibot-isam007`
   -- `okteto deploy fastapi --build --timeout 10m` (!!! timeout is super important here as it gives sentence_transformer enough time to load!!!)
   -- `okteto deploy chatbot action-server rasa --build`

7. That's it! Check the deployment on the okteto dashboard and test fastapi link to make sure it's listenning on the right port. 
   !!! Note, even though Okteto says your containers are running, it does take more time after that for them to complete their initialization, 
       so make sure to wait until all server logs confirm that they run.