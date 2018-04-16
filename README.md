# Gist-guide
# 1. Git Auto Completion
Nếu chạy nhiều câu lệnh Git qua dòng lệnh, Thật là một công việc tẻ nhạt mỗi lần gõ các lệnh bằng tay.
Để giúp đỡ việc này, bạn có thể tự động hoàn thành lệnh Git trong vòng vài phút.
Để có được bản script này, hãy chạy lệnh sau trong hệ thống Unix:

cd ~
curl https://raw.github.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash

Next, add the following lines to your ```~/.bash_profile``` file:

    if [ -f ~/.git-completion.bash ]; then
      . ~/.git-completion.bash
    fi

Mặc dù tôi đã đề cập đến điều này trước đây, nhưng tôi không thể nhấn mạnh nó đủ:
Nếu bạn muốn sử dụng các tính năng của Git một cách đầy đủ, bạn chắc chắn nên chuyển sang giao diện dòng lệnh!
# 2. Bỏ qua File trong Git
Bạn có mệt mỏi với các tập tin biên dịch (như .pyc) xuất hiện trong repo Git của bạn? 
Hay bạn có bực vì bạn đã lỡ thêm chúng vào Git? Không cần nhìn đâu xa,
có một cách mà bạn có thể nói với Git để bỏ qua hoàn toàn một số tập tin và thư mục.
Đơn giản chỉ cần tạo một tệp với tên ```.gitignore``` và liệt kê các tệp tin và thư mục mà bạn không muốn Git theo dõi.
Bạn có thể tạo ngoại lệ bằng cách sử dụng dấu chấm than (!).
    
    *.pyc
    *.exe
    my_db_config/
    !main.pyc

# 3. Ai đã làm rối code của tôi?
Đó là bản năng tự nhiên của con người để đổ lỗi cho người khác khi có điều gì đó không ổn.
Nếu máy chủ của bạn bị hỏng, Rất dễ để tìm ra thủ phạm — chỉ cần thực hiện  ```git blame```.
Câu lệnh này sẽ cho bạn thấy tác giả của từng câu lệnh trong file, 
commit thực hiện thay đổi cuối cùng của dòng đó, và mốc thời gian của commit.
```git blame [file_name]```
# 4. Xem lại lịch sử của Repository
Chúng tôi đã xem xét việc sử dụng ```git log``` trong một hướng dẫn trước đó, tuy nhiên, có ba lựa chọn mà bạn cần biết.
        
        ```--oneline``` – Nén thống tin hiện thỉ bên cạnh mỗi commit thành các commit hash giảm thiểu và các thông điệp commit, 
        tất cả được hiển thị trong 1 dòng đơn
        ```--graph``` – Lựa chọn này vẽ 1 miêu tả đồ thị dựa trên văn bản về lịch sử trên phía tay trái của đầu ra. 
        Nó sẽ vỗ nghĩa nếu bạn đang xem lịch sử cho 1 nhánh đơn
        ```--all``` – Hiển thị lịch sử của tất cả các nhánh.
        
Dưới đây là những gì kết hợp các tùy chọn như sau:

# 5. Không bao giờ mất theo dõi của một commit
Hãy nói rằng bạn đã commit cái gì đó mà bạn không muốn và kết thúc bằng việc thực hiện hard reset để quay trở lại trạng thái trước. 
Gần đây, bạn nhận ra bạn đã sót vài thông tin khác trong tiến trình và muốn lấy nó lại, hay ít nhất là xem nó. 
Đây là lúc ```git reflog``` có thể giúp bạn.
Một ```git log``` đơn giản cho bạn biết commit mới nhất, cha của nó, cha của cha nó, và hơn nữa. 
Tuy nhiên, ```git reflog``` là một danh sách các commit chỉ được trỏ vào phần tử đầu.
Nhớ rằng nó là một hệ thống local của bạn;nó không phải là một phần repository  của bạn và không bao gồm các pushes hoặc merges.
Nếu tôi chạy ```git log```, Tôi nhận được những commit cái mà là một phần của repository của tôi:
Tuy nhiên, Một ```git reflog``` hiển thị 1 commit bị mất khi bạn thực hiện 1 hard reset:
# 6. Phân laoij các phần của file đã thay đổi cho một Commit
Nói chung là tạo các commit dựa trên chức năng, đó là mỗi commit phải đại diện cho một chức năng hoặc một bug fix. 
Hãy xem xét điều gì sẽ xảy ra nếu bạn sửa hai lỗi hoặc thêm nhiều tính năng mà không thực hiện commit nào.
Trong trường hợp tình huống như vậy, bạn có thể đặt những thay đổi trong một cam kết duy nhất.
Nhưng có một cách tốt hơn: Phân loại các tập tin riêng lẻ và commit chúng một cách riêng biệt.
Giả sử bạn đã thực hiện nhiều thay đổi cho một tệp và muốn chúng xuất hiện trong các commit riêng biệt.
Trong trường hợp này, chúng ta thêm file với tiền tố `-p` để thêm các câu lệnh.
        git add -p [file_name]
Chúng ta hãy cùng nhau chứng minh điều đó.
Tôi đã thêm ba dòng mới vào file_name và tôi chỉ muốn các dòng đầu tiên và thứ ba xuất hiện trong cam kếtcommit của tôi.
Hãy xem những gì một ```git driff``` cho chúng ta thấy.
Và hãy xem điều gì sẽ xảy ra khi chúng ta thêm tiền tố -p vào lệnh add của chúng ta.
Có vẻ như Git cho rằng tất cả những thay đổi đều là một phần của cùng một ý tưởng, do đó nhóm nó thành một khối lớn. 
Bạn có các lựa chọn sau:
    Nhập y để phân loại nhóm này
    Nhập n để không phân loại
    Nhập e để tự sửa nhóm này
    Nhập d để thoát hoặc tới dòng tiếp theo
    Nhập s dể chia nhóm.
Trong trường hợp của chúng tôi, 
chúng tôi chắc chắn muốn chia nhỏ nó thành các phần nhỏ hơn để bổ sung có chọn lọc và bỏ qua phần còn lại.
Như bạn thấy, chúng tôi đã thêm vào dòng đầu tiên và thứ ba và bỏ qua thứ hai.
Sau đó bạn có thể xem tình trạng của repo và thực hiện một commit.
# 7. Nén nhiều commit
Khi bạn gửi code của mình để xem xét và tạo một pull request (thường xảy ra trong các dự án mã nguồn mở),
bạn có thể được yêu cầu thay đổi cho mã của bạn trước khi nó được chấp nhận.
Bạn tạo sự thay đổi, chỉ khi được yêu cầu thay đổi nó 1 lần nữa trong lần xem lại tiếp theo. 
Trước khi bạn biết nó, bạn có vài commit thêm. 
Lý tưởng nhất là bạn có thể ép chúng lại làm 1 sử dụng câu lệnh ```rebase```.
        git rebase -i HEAD~[number_of_commits]
Nếu bạn muốn nén 2 commit cuối, câu lệnh bạn chạy như dưới đây.
        git rebase -i HEAD~2
Khi chạy lệnh này, bạn sẽ được đưa đến một giao diện tương tác liệt kê các cam kết và hỏi bạn những cái cần nén.
Tốt nhất là bạn chọn những commit mới nhất và sử dụng những cái cũ.
Sau đó bạn đươc hỏi cung cấp một commit message mới cho commit mới.  Quá trình này chủ yếu viết lại lịch sử commit của bạn.
# 8. Cất những thay đổi chưa được commit
Hãy nói rằng bạn đang làm việc trên 1 tính năng hay 1 lỗi cụ thể, và bạn bỗng nhiên được yêu cầu mô tả công việc của bạn. 
Công việc hiện tại của bạn không hoàn thiện đủ để được commit, 
và bạn không thể đưa ra nhưng mô tả tại nhóm này( mà không trở về các thay đổi). 
Trong trường hợp này, ```git stash``` tới để giải cứu bạn. 
Stash bản chất lấy tất cả các thay đổi của bạn và lưu trữ chúng để sử dụng sau này. 
Để cất những thay đổi của bạn, bạn chỉ đơn giản chạy lệnh sau.
        
        git stash
        
Trong màn hình chụp cuối cùng, bạn có thể thấy rằng mỗi stash có 1 định danh, 
1 số duy nhất (mặc dù chúng tôi chỉ có duy nhất 1 stash trong trường hợp này). 
Trong trường hợp bạn muốn gọi chỉ duy nhất stash được chọn., bạn thêm định đặc tả cho câu lệnh ```apply```

        git stash apply stash@{2}
        
# 9. Kiểm tra các commit bị mất
mặc dù ```reflog``` là một cách kiểm tra các commit bị mất, nó không khả thi trong các repo lớn. 
Đây là khi câu lệnh fsck (file system check) có hiệu lực.
        git fsck --lost-found
Ở đây bạn có thể thấy các commit bị mất. 
Bạn có thể kiểm tra các thay đổi trong commit bằng cách chạy ```git show [commit_hash]``` hoặc
khôi phục nó bằng cách chạy ```git merge [commit_hash]```.
```git fsck``` có 1 lợi thế hơn ```reflog```. 
Hãy nói rằng bạn đã xóa 1 branch remote và sau đó clone repository. 
Với ```fsck``` bạn có thể tìm kiếm và khôi phục các nhánh remote bị xóa.

# 10. Cherry Pick
Cuối cùng tôi đã lưu các lệnh Git thanh lịch nhất. 
Lệnh cherry-pick là lệnh Git yêu thích của tôi, bởi vì nghĩa đen cũng như tiện ích của nó!
Theo cách đơn giản nhất, cherry-pickchọn một commit duy nhất từ một nhánh khác và kết hợp nó với cái hiện tại của bạn.
Nếu bạn đang làm việc theo kiểu song song trên hai hoặc nhiều nhánh, 
bạn có thể nhận thấy một lỗi xảy ra ở tất cả các nhánh.
Nếu bạn giải quyết nó trong một, bạn có thể cherry-pick commit vào các nhánh khác,
mà không phiền với các tập tin hoặc các commit khác.
Tôi có 2 nhánh và tôi muốn ```cherry-pick``` commi ts```b20fd14: Cleaned junk``` đến 1 nhánh khác.
Tôi chuyển tới nhánh tới nhánh tôi muốn ```cherry-pick``` commit, và chạy lệnh sau:
        git cherry-pick [commit_hash]
Mặc dù lần này tôi đã dọn ```cherry-pick```, bạn nên biết rằng cây lệnh này thường dẫn tới các xung đột, 
vì vậy sử dụng nó cẩn thận.

# Kết luận
Với những điều này, mẹo cuối của chúng tôi mà tôi nghĩ rằng 
có thể giúp bạn lấy kỹ năng Git của bạn đến một cấp độ mới. 
Git là thứ tốt nhất ngoài đó và nó có thể  hoàn thành bất cứ thứ gì mà bạn có thể tưởng tượng. 
Vì thế, hãy luốn cố gắng thách thức bản thân với Git. Cơ hội đến, bạn sẽ có thể học được điều gì đó mới mẻ!
