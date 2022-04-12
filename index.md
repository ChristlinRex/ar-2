!doctype html>
<html>
    <head>
        <script src="https://aframe.io/releases/1.0.4/aframe.min.js"></script>
        <script src="https://raw.githack.com/AR-js-org/AR.js/master/aframe/build/aframe-ar.js"></script>
        <script src="https://raw.githack.com/AR-js-org/studio-backend/master/src/modules/marker/tools/gesture-detector.js"></script>
        <script src="https://raw.githack.com/AR-js-org/studio-backend/master/src/modules/marker/tools/gesture-handler.js"></script>
        <script>
            AFRAME.registerComponent('videohandler', {
                init: function () {
                    var marker = this.el;
                    this.vid = document.querySelector("#vid");

                    marker.addEventListener('markerFound', function () {
                        this.toggle = true;
                        this.vid.play();
                    }.bind(this));

                    marker.addEventListener('markerLost', function () {
                        this.toggle = false;
                        this.vid.pause();
                    }.bind(this));
                },
            });
        </script>
    </head>

    <body style="margin: 0; overflow: hidden;">
        <a-scene
            vr-mode-ui="enabled: false"
            loading-screen="enabled: false;"
            arjs='sourceType: webcam; debugUIEnabled: false;'
            id="scene"
            embedded
            gesture-detector
        >
            <a-assets>
                <video
                    id="vid"
                    src="assets/asset.mp4"
                    preload="auto"
                    response-type="arraybuffer"
                    loop
                    crossorigin
                    webkit-playsinline
                    autoplay
                    muted
                    playsinline
                ></video>
                <img crossorigin="anonymous" id="linkedinTexture" src="https://cdn.glitch.com/6f8b5a13-fd4d-445d-b9eb-57c735d720ea%2FPostLinkedin.png?1528821333139">
            </a-assets>

            <a-marker
                type="pattern"
                preset="custom"
                url="assets/marker.patt"
                videohandler
                smooth="true"
                smoothCount="10"
                smoothTolerance="0.01"
                smoothThreshold="5"
                raycaster="objects: .clickable"
                emitevents="true"
                cursor="fuse: false; rayOrigin: mouse;"
                id="markerA"
            >
                <a-video
                    src="#vid"
                    scale="1 1 1"
                    position="0 0.1 0"
                    rotation="-90 0 0"
                    class="clickable"
                    gesture-handler
                ></a-video>
                <a-link class="clickable" href="https://www.linkedin.com/in/pierpaolo28/" title="" image="" position="-1.4 0.0 0.333" rotation="-67.42 0 0" scale="0.6 0.6 0.6" geometry="primitive:circle;segments:64" material="shader:portal;side:double;visible:false" link="title:.">
                        <a-box scale="0.8 0.8 1.05" material="src:#linkedinTexture" position="-0.09854454977856898 -0.0036935886841299587 -0.2155814669584256" radius="2" segments-height="84" rotation="-23.450000000000003 0 0" geometry="">
            </a-marker>

            <a-entity camera></a-entity>
        </a-scene>
    </body>
</html>
