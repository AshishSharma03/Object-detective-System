https://angry-tesla-845375.netlify.app/

Using a machine learning toolkit of your choice, create a tool which identifies objects in the image, then returns positions in pixels corresponding to bounding boxes of a user-selected class of object in the image. For example, given an image with both cats and dogs, return bounding boxes for only cats.

![working_gif](/Screenshots/1.gif)

Added a Specific Class Input to enter one of the 90 classes in the COCO dataset. The predictions will be filtered and only that class will be shown.

```
model
  .detect(document.getElementById("webcamFeed"))
  .then(predictions => {
    if (specificClass === "") {
      setPredictions(predictions);
    } else {
      const specificDetections = predictions.filter(
        p => p.class === specificClass
        );
      console.log(specificDetections);
      setPredictions(specificDetections);
    }
  })
```

## Live Demo - [Click Here](https://angry-tesla-845375.netlify.com/)

1. Wait for the Model to load
2. Allow access to the Webcam
3. Click the 'Capture Photo' button to log a base64 string of the Webcam frame
4. Click 'Predict' button to get a Predictions
5. Type a Class Name to filter the Predictions for that specific Class

Note: Please Click the canvas to load a Webcam frame onto the canvas. Sorry but I couldn't make the `useRef()` hook work correctly. I will fix this soon!

---

# React.js and Tensorflow.js Object Detection

A React Web Application to test the COCO SSD pre-trained model to detect objects through the User's Webcam or other video source. Uses Tensorflow.js to run the model directly in the browser.

![working](/Screenshots/0.png)

## [Object Detection (coco-ssd)](https://www.npmjs.com/package/@tensorflow-models/coco-ssd)

Object detection model that aims to localize and identify multiple objects in a single image.

This model is a TensorFlow.js port of the COCO-SSD model. For more information about Tensorflow object detection API, check out this readme in [tensorflow/object_detection](https://github.com/tensorflow/models/blob/master/research/object_detection/README.md).

This model detects objects defined in the COCO dataset, which is a large-scale object detection, segmentation, and captioning dataset. You can find more information [here](http://cocodataset.org/#home). The model is capable of detecting [90 classes of objects](https://github.com/tensorflow/tfjs-models/blob/HEAD/src/classes.ts). (SSD stands for Single Shot MultiBox Detection).

### Usage

```
const [model, setModel] = useState(null);
const [predictions, setPredictions] = useState(null);

useEffect(() => {
    const loadModel = async () => {
      const newModel = await cocoSsd.load({ base: "lite_mobilenet_v2" });
      setModel(newModel);
    };
    loadModel().then(setIsModelLoaded(true));
  }, []);

model.detect(document.getElementById("webcamFeed"))
    .then(predictions => {
        setPredictions(predictions);
    })
```

Sample Output of the `model.detect()` method

```
[{
  bbox: [x, y, width, height],
  class: "person",
  score: 0.8380282521247864
}, {
  bbox: [x, y, width, height],
  class: "kite",
  score: 0.74644153267145157
}]
```

## Future Improvements:

1. Because of Tensorflow.js we can offer a option to the user to dynamically change the model which is being used for Object Detection.
2. The user can save the image with detections with a Right Click > Save Image As. Adding a dedicated Download button will simplify this process.
3. As we have the box co-ordinates of the detected object which we use to paint in the canvas, we should be able to cut out the portion of the image and offer cropped views of the image for the user.

## Resources:

- [Create a New React App](https://reactjs.org/docs/create-a-new-react-app.html) - Get started with React here
- [Material-UI](https://material-ui.com/) - React components for faster and easier web development
- [TensorFlow.js](https://www.tensorflow.org/js) - A library for machine learning in Javascript
- [React Webcam](https://www.npmjs.com/package/react-webcam) - Webcam component for React

## References:

- https://github.com/juandes/tensorflowjs-objectdetection-tutorial
- https://github.com/DhruvJawalkar/tensorflow.js-multiple-object-detection
- https://github.com/overflowjs-com/image_object_detection_tensor_api
- https://github.com/leartgjoni/webcam-object-detection

## Available Scripts:

In the project directory, you can run: `yarn start`

Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

---

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
