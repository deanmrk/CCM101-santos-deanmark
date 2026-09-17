# Reflection
---------------------
For me, the docker containers are faster than virtual machines because they do not need a full operating system to run. And the virtual machines take longer to boot since they load an entire OS, while containers start quickly by sharing the host system. Because of this, containers are more efficient and are better suited for modern applications that need fast deployment.

Port mapping such as -p 8080:80 allows the container to be accessed from the host machine. It connects a port from the host (8080) to a port inside the container (80). Without this, the web server running inside the container would not be reachable from outside, making it useless for users who want to access the application.

When using docker rm, the container is completely removed along with its stored data. This shows that containers are temporary by default. If important data is needed, it must be saved using volumes or external storage, otherwise it will be lost once the container is deleted.

The containerization improves collaboration between developers and IT operations. Developers can build applications in containers, and operations teams can deploy them without worrying about compatibility issues. This ensures consistency across different environments such as development, testing, and production.

My GitHub portfolio is improving as I complete more laboratory activities. It shows my progress in learning cloud computing and helps me organize my work properly. It also serves as proof of my skills, which can be useful in the future when applying for jobs or internships.

----------------------------
