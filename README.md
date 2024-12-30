<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Audio Visualizer</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.0/p5.js"></script>
</head>
<body>
    <script>
        let mic;
        let fft;

        function setup() {
            createCanvas(windowWidth, windowHeight);
            mic = new p5.AudioIn();
            mic.start();
            fft = new p5.FFT();
            fft.setInput(mic);
        }

        function draw() {
            background(0);
            let spectrum = fft.analyze();

            // Draw the waveform
            noFill();
            stroke(255);
            beginShape();
            for (let i = 0; i < spectrum.length; i++) {
                let x = map(i, 0, spectrum.length, 0, width);
                let y = map(spectrum[i], 0, 255, height, 0);
                vertex(x, y);
            }
            endShape();
        }

        function windowResized() {
            resizeCanvas(windowWidth, windowHeight);
        }
    </script>
</body>
</html>
