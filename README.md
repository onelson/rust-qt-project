Yet another project-oriented docker-compose environment.

This time, it's for doing rust/Qt development, using
https://github.com/KDE/rust-qt-binding-generator (which I have rudely 
pre-compiled and dropped in the bin dir).

Largely a mash-up of rustup-base and rustup-project, with env vars in place to
permit the container to run processes that need X11 on your desktop session. 
