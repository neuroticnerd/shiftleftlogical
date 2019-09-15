:date: 2019-09-09
:modified: 2019-09-09

======================================
Flask Notes
======================================

.. code-block:: python

    # https://stackoverflow.com/questions/38048355/large-file-upload-in-flask
    # https://stackoverflow.com/questions/15040706/streaming-file-upload-using-bottle-or-flask-or-similar

    @app.route("/upload/<filename>", methods=["POST", "PUT"])
    def upload_process(filename):
        filename = secure_filename(filename)
        filepath_full = os.path.join(application.config['UPLOAD_FOLDER'], filename)
        with open(filepath_full, "wb") as f:
            chunk_size = 4096
            while True:
                chunk = flask.request.stream.read(chunk_size)
                if len(chunk) == 0:
                    return

                f.write(chunk)
        return jsonify({'filename': filename})
