# ImageResizer
Redimensionamento de Imagens com Azure Functions + Image Resizer e Blob Trigger 

project.json

{
	"frameworks": 
	{
		"net46":
		{
			"dependencies": 
			{
				"ImageResizer": "4.0.5"
			}
		}
	}
}

run.csx

using ImageResizer;
using ImageResizer.ExtensionMethods;
 
public static void Run(Stream myBlob, 
					   string blobname, 
					   string blobextension, 
					   Stream outputBlob, 
					   TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{blobname} \n Size: {myBlob.Length} Bytes");
    
    var instructions = new Instructions
    {
        Width = 200,
        Mode = FitMode.Carve,
        Scale = ScaleMode.Both
    };
    ImageBuilder.Current.Build(new ImageJob(myBlob, outputBlob, instructions));
}
