# myfirst

the first demo to use github  with mvc5

#build database by ef code first

#use default identity table

public static Image GetQRCode(string data)
        {
            //生成二维码 
            string qrEncoding = "Byte";
            string Level = "M";
            //用ThoughtWorks.QRCode生成二维码时出现“索引超出了数组界限”的错误。
            string txt_ver = "0";
            string txt_size = "4";

            ThoughtWorks.QRCode.Codec.QRCodeEncoder qrCodeEncoder = new ThoughtWorks.QRCode.Codec.QRCodeEncoder();
            String encoding = qrEncoding;
            if (encoding == "Byte")
            {
                qrCodeEncoder.QRCodeEncodeMode = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ENCODE_MODE.BYTE;
            }
            else if (encoding == "AlphaNumeric")
            {
                qrCodeEncoder.QRCodeEncodeMode = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ENCODE_MODE.ALPHA_NUMERIC;
            }
            else if (encoding == "Numeric")
            {
                qrCodeEncoder.QRCodeEncodeMode = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ENCODE_MODE.NUMERIC;
            }
            try
            {
                int scale = Convert.ToInt16(txt_size);
                qrCodeEncoder.QRCodeScale = scale;
            }
            catch (Exception ex)
            {
                return null;
            }
            try
            {
                int version = Convert.ToInt16(txt_ver);
                qrCodeEncoder.QRCodeVersion = version;
            }
            catch (Exception ex)
            {
                return null;
            }
            string errorCorrect = Level;
            if (errorCorrect == "L")
                qrCodeEncoder.QRCodeErrorCorrect = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ERROR_CORRECTION.L;
            else if (errorCorrect == "M")
                qrCodeEncoder.QRCodeErrorCorrect = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ERROR_CORRECTION.M;
            else if (errorCorrect == "Q")
                qrCodeEncoder.QRCodeErrorCorrect = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ERROR_CORRECTION.Q;
            else if (errorCorrect == "H")
                qrCodeEncoder.QRCodeErrorCorrect = ThoughtWorks.QRCode.Codec.QRCodeEncoder.ERROR_CORRECTION.H;

            Image image;
            qrCodeEncoder.QRCodeForegroundColor = Color.Black;//二维码颜色
            image = qrCodeEncoder.Encode(data, System.Text.Encoding.UTF8);
            return image;
        }
