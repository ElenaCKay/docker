# Use the official Node.js image as the base image
FROM node:12

 

# Set the working directory inside the container
WORKDIR /app

 
# Add environment variables

ENV DB_HOST=mongodb://172.17.0.2:27017/posts 

# Copy the package.json and package-lock.json files to the container
COPY package*.json ./

# Install app dependencies
RUN npm install


# Copy the rest of the application code to the container
COPY app/app /app

# Expose the port that the Node.js app is listening on
EXPOSE 3000


# Command to start the Node.js application
CMD ["npm", "start"]
